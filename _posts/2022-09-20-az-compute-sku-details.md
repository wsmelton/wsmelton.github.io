---
layout: post
title: Azure PowerShell - Get-AzComputeResourceSku
---

## Compute Resource Skus

I have bookmarks on almost any machine I’m using for work that point to the Sku details for both Virtual Machines and Disks:

- [Virtual Machine Sizes](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes?WT.mc_id=CDM-MVP-5002856)

- [Azure Managed Disk Types](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types?WT.mc_id=CDM-MVP-5002856)

The above pages give you a table view of the Virtual Machine skus and the disk types (e.g. HHD, SSD, SSD v2). They are a constant reference when I’m working on sizing a new project that requires any virtual machine. I wanted to get this all into Excel so I could more easily reference it. I also use Excel to size out builds to ensure I’m meeting capacity and throughput requirements for vendor solutions/products.

## PowerShell script

The below script will use `Get-AzComputeResourceSku` command to pull the details from the REST API and dump that into an Excel file.

<script src="https://gist.github.com/wsmelton/3c2984918106d808027a38b60f2ece06.js"/></script>
