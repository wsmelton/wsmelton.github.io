---
layout: post
title: Installing SSRS on Server Core
categories: sql, lab
---

# Lab Case

I need to install SQL Server Reporting Services (SSRS) on Window Server 2019 Core (non-gui).

## Steps

1. Download installer:

    SSRS has to be downloaded separately from the SQL Server media. You can find that download [here](https://www.microsoft.com/en-us/download/details.aspx?id=100122)

1. Server Core allows for the installer wizard to be used, put the `exe` on the server and run it.
1. Complete the install wizard.
1. Once the installation completes run the configuration tool using the following command:

    ```console
    & 'C:\Program Files\Microsoft SQL Server Reporting Services\Shared Tools\RSConfigTool.exe'
    ```

1. Complete the configuration options desired.
