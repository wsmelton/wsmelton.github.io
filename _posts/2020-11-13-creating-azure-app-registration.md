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

## Challenge

In order to use that app registration requires it to be provided permissions for the services you need your application or integration. No real reason to just have an app with no rights, right?

Searching through the Internet you will find some examples of using Azure CLI (`az`) or even API calls directly to things like the Microsoft Graph API service. The end result I got to was simply grabbing the Service Principal and within that object are the role information you will need.

So for my use case I needed Microsoft Graph.
