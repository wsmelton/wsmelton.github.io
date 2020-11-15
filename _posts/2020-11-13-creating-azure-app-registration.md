---
layout: post
title: Creating an Azure App Registration with AzureAd
categories: azure, powershell
---

Allowing applications access to your Azure tenant is generally done by creating an [Azure App Registrations](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/walkthrough-register-app-azure-active-directory).

Going through a tutorial is nice if you want to click, click through the portal. I fashion doing things using PowerShell as it helps to make it consistent, especially if you need to do this for multiple tenants.

## AzureAD Module Commands/Types

The main commands I used in this process from the module:

- `Get-AzureADServicePrincipal`
- `New-AzureADApplication`
- `New-AzureADApplicationPasswordCredential`
- `Microsoft.Open.AzureAD.Model.RequiredResourceAccess`
- `Microsoft.Open.AzureAD.Model.ResourceAccess`

## Role IDs

One key piece of information you need when creating an app registration with `New-AzureADApplication` is the role IDs for the permissions you want to assign. I mean after all, if it does not have permissions to do anything why would you need it anyway :shrug:. Searching through the Internet I found mostly references to using `az` CLI and dumping data to JSON file. Which can work but I wanted to make this script more dynamic, and also base it off the readable name of the permission; just as you would find in the portal.

In the end I found easiest way to get this information was using `Get-AzureADServicePrincipal`. 

Searching through the Internet you will find some examples of using Azure CLI (`az`) or even API calls directly to things like the Microsoft Graph API service. The end result I got to was simply grabbing the Service Principal and within that object are the role information you will need. The below code provides that list of roles I need in my use case:

```powershell
$appPerms = 'Group.Read.All','GroupMember.Read.All','Member.Read.Hidden','User.Read.All'
Get-AzureADServicePrincipal -Filter "DisplayName eq 'Microsoft Graph'"
$permissions = $msGraphService.AppRoles.Where({$_.Value -in $appPerms})
```

## RequiredResourceAccess Object

The object type required for assigning permissions, when you create the app registration, is the `Microsoft.Open.AzureAD.Model.RequiredAccess` type. This type is available to you when the AzureAD module is loaded into your session. To create this an assign those roles I pulled from above requires you to simply iterate over each role and add it to the object property `ResourceAccess`. I did that using this code:

```powershell
$msGraphResourceAccess = New-Object -TypeName "Microsoft.Open.AzureAD.Model.RequiredResourceAccess"
$msGraphResourceAccess.ResourceAppId = $msGraphService.AppId
foreach ($p in $permissions) {
    $appPermissions = New-Object -TypeName "Microsoft.Open.AzureAD.Model.ResourceAccess" -ArgumentList $p.Id,"Role"
    #Add the role to the resource access object
    $msGraphResourceAccess.ResourceAccess += $appPermissions
}
```

After that I added additional settings I needed and then passed those values to the command.
