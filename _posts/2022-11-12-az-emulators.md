---
layout: post
title: Azure Cloud Service Emulators
---

<a href="https://www.flaticon.com/free-icons/travel" title="travel icons"><img src="https://user-images.githubusercontent.com/11204251/201482432-a757fffb-c2e0-4b36-9fd1-5db1902ea67a.png" alt="Travel icons created by Icongeek26 - Flaticon" width="150"></a>

Air plane mode, a required setting if you travel in an airplane. Depending on where you are going whether it is for work, school, vacation, or because I want to you may have a lot of time on your flight. Are you looking to learn more about Azure's cloud services? Want to change careers to be a developer? Did you Azure offers the ability for you to develop against some of their services in 100% offline mode? You don't even need an Internet connection.

If you have already started your journey developing against Azure you may already be aware of the amazing list of [Azure Developer tools](https://azure.microsoft.com/en-us/downloads/).

## Azure Emulators

Below are a list of emulators that Azure offers at the time of writing. Please review documentation and EULA to identify any special requirements or limitations on approved usage. In most cases these are for development purposes only, some you can use with your testing pipelines.

- [Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/local-emulator?WT.mc_id=CDM-MVP-5002856)
    Allows you to have a local environment that emulates the Azure Cosmos DB service. It also supports migrating data between the emulator and Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).

- [Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/local-dev-experience-sql-database-emulator?WT.mc_id=CDM-MVP-5002856)
    This one will require Docker as the emulator is a containerized application that will run on your local system. You have the option when you spin the emulator up to do Full or Lite. Lite has the smallest footprint image and is based on Azure SQL Edge's base image. There are some features in Azure SQL that are [not supported](https://learn.microsoft.com/en-us/azure/azure-sql/database/local-dev-experience-sql-database-emulator?view=azuresql#limitations&WT.mc_id=CDM-MVP-5002856). You can use this for automation testing as well in your deployment pipelines.

- [Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azurite?tabs=visual-studio-code&WT.mc_id=CDM-MVP-5002856)
    The new version uses Azurite platform is cross-platform supported, and this supersides the old [Azure Storage Emulator](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-emulator?WT.mc_id=CDM-MVP-5002856). This can also be used in your deployment pipelines.

- [Azure Function Apps](https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local#local-development-environments?WT.mc_id=CDM-MVP-5002856)
    This one would not be a true "emulator" but provides a local environment runtime that allows you to execute and spin up your Function App without having to be connected to the Azure Cloud service. It also supports communicating with the emulators above for a complete development environment.
