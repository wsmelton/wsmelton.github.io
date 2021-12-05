---
layout: post
title: Map Azure Data Disk to VM Disk and Volume
---

## Lab Case

I need to expand an Azure Storage Account disk that is attached to a particular drive letter in the Azure VM (Windows Server).

### Solution

There are steps that can be used to gather this data from the UI in Windows Server utilizing the Disk Management console, but PowerShell is much more efficient in this use case.

The output of the script below will look similar to the following:

```console
AzureVMName    AzureDiskName             DriveLetter LUN PartitionName          PartitionSizeGB DiskIndex SCSILogicalUnit DiskSizeGB DiskStatus
-----------    -------------             ----------- --- -------------          --------------- --------- --------------- ---------- ----------
VM004DB        vm004db-datadisk1         E             0 Disk #2, Partition #0              128         2               0        128 OK
VM004DB        vm004db-datadisk2         F             1 Disk #3, Partition #0             4090         3               1       4090 OK
VM004DB        vm004db-datadisk3         G             2 Disk #4, Partition #0             4090         4               2       4090 OK
```

```powershell
<#
    .SYNOPSIS
    Returns a table providing mapping of Azure Storage disk to Azure VM OS volume.

    .DESCRIPTION
    Script is written to be executed from the admin's local device (adjust to execute through Azure Function or Runbook as desired)
    Items/Dependencies:
    - Az CLI (quickest one-liner to get the data)
    - PowerShell (Windows PowerShell 5.1 or PowerShell 7+)
    - Network access to Azure VM via WinRM
    - Azure Account privileges to query VM data
    - Also assumes the VM name is also the hostname for WinRM access

    . EXAMPLES
    .\Get-AzDiskToVmDisk.ps1 -VMName VM004DB -ResourceGroup mystuff -Credential (Get-Secret myAdmin)

    Uses SecretManagement module to retrieve PSCredential for "myAdmin".
    Pulls the list of Storage disk assigned to VM "VM004DB", CIM calls to map those to the Disk and Volume in Windows Server

    .NOTES
    Original source: https://github.com/peterlil/script-and-templates/blob/master/az%20cli/iaas/storage/map-azure-disks-to-vm-disks-windows.ps1
#>
param(
    [string] $VMName,
    [string] $ResourceGroup,
    [PSCredential]$Credential
)

<# Create CIM Session to the provided VM using the credential #>
try {
    $cimSession = New-CimSession -ComputerName $VMName -Credential $Credential
} catch {
    throw "Unable to connect CIM to $VMName $($_)"
}

<# Grab the Disk name and LUN number for the VM in Azure #>
$azDisks = az vm show -n $VMName -g $ResourceGroup --query "storageProfile.dataDisks[].{Name:name, LUN:lun}" --output JSON | ConvertFrom-Json

<# Using the CIM Session retrieve disk, partition and volume details from Windows Server #>
$diskDrives = Get-CimInstance -Class Win32_DiskDrive -CimSession $cimSession | Sort-Object -Property DeviceID
$diskDriveToDiskPartitionMappings = Get-CimInstance -Class Win32_DiskDriveToDiskPartition -CimSession $cimSession
$diskPartitions = Get-CimInstance -Class Win32_DiskPartition -CimSession $cimSession
$logicalDiskToPartitionMappings = Get-CimInstance -Class Win32_LogicalDiskToPartition -CimSession $cimSession
$logicalDisks = Get-CimInstance -Class Win32_LogicalDisk -CimSession $cimSession

foreach ($diskDrive in $diskDrives) {
    if ($diskDrive.InterfaceType -eq 'SCSI') {
        # Get partition mappings for the current drive
        $diskDriveToDiskPartitionMapping = $diskDriveToDiskPartitionMappings | Where-Object { $_.Antecedent.DeviceID -eq $diskDrive.DeviceID }

        $azDiskName = ($azDisks | Where-Object { $_.LUN -eq $diskDrive.SCSILogicalUnit }).Name

        if($diskDriveToDiskPartitionMapping) {
            $diskDriveToDiskPartitionMapping | ForEach-Object {
                $partitionMapping = $_
                $diskPartition = $diskPartitions | Where-Object { $_.Name -eq $partitionMapping.Dependent.DeviceID }

                $logicalDiskToPartitionMapping = $logicalDiskToPartitionMappings | Where-Object { $_.Antecedent.DeviceID -eq $partitionMapping.Dependent.DeviceID }

                if($logicalDiskToPartitionMapping) {
                    $logicalDisk = $logicalDisks | Where-Object { $_.DeviceID -eq $logicalDiskToPartitionMapping.Dependent.DeviceID }
                }

                if($logicalDisk.DeviceID) {
                    $deviceId = $logicalDisk.DeviceID.Trim(':')
                }
                [pscustomobject]@{
                    AzureDiskName   = $azDiskName
                    DriveLetter     = $deviceId
                    LUN             = $DiskDrive.SCSILogicalUnit
                    PartitionName   = $diskPartition.Name
                    PartitionSizeGB = [math]::Round($diskPartition.Size / 1GB, 1)
                    DiskIndex       = $DiskDrive.Index
                    SCSILogicalUnit = $DiskDrive.SCSILogicalUnit
                    DiskSizeGB      = [math]::Round($DiskDrive.Size / 1GB)
                    DiskStatus      = $DiskDrive.Status
                }
            }
        }
        $logicalDisk,$logicalDiskToPartitionMapping,$diskDriveToDiskPartitionMapping,$deviceId,$diskPartition = $null
    }
}
```