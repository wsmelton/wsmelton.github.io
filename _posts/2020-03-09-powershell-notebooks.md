---
layout: post
title: PowerShell Notebooks with dotnet interactive
---

In February the preview of [dotnet interactive](https://devblogs.microsoft.com/dotnet/net-interactive-is-here-net-notebooks-preview-2/) was announced. Along with that the PowerShell team worked with them on the Net-PowerShell kernel as well. This is all packaged together. In this post I'm just going to provide the quick steps that can be used to get everything installed, and also to update it to make sure you have the latest bits and features.

## Requirements

1. [Python](https://www.python.org/downloads) (_I'm using Python 3.8.2 release._)
1. [.NET 3.1 SDK](https://dotnet.microsoft.com/download) (_if you have Visual Studio installed you likely already have this_)

### Python Installation Notes

- When you run the installer for Python, make sure you check the box for adding/updating your system `PATH`. This will help where you can simply call `python` from any command prompt on your system.
- Also ensure you include `pip` in the installation. The download above for Python will include that for you, `pip` is the package manager for Python and is needed to get dotnet-interactive installed.

Once the installation is completed you can confirm everything is in working order by running the two commands below in a PowerShell console:

```console
dotnet --version
python --version
pip --version
```

The output from the above commands will ensure everything is in place to continue. If one of the commands above does not output version information then you will need to troubleshoot accordingly for your system.

A sample output from my system:

```powershell
❯ pip --version
>> python --version
>> dotnet --version
pip 19.2.3 from c:\users\smelton\appdata\local\programs\python\python38\lib\site-packages\pip (python 3.8)
Python 3.8.2
3.1.101
```

### Setup

The following steps will be taken now and can be run from a PowerShell console to finish the setup:

1. Install JupyterLab --> `pip install jupyterlab`
1. Install Notebook --> `pip install notebook`
1. Install dotnet interactive --> `dotnet tool install -g --add-source "https://dotnet.myget.org/F/dotnet-try/api/v3/index.json" Microsoft.dotnet-interactive`

### Update

Like any other software you use on your system it is always good to keep it updated. With dotnet interactive being just released there will be times that new functionality or performance improvements are released. The following will keep you updated with the latest bits:

1. Update jupyterlab --> `pip install -U jupyterlab`
1. Update Notebook --> `pip install -U notebook`
1. Update dotnet internactive --> `dotnet tool update -g --add-source "https://dotnet.myget.org/F/dotnet-try/api/v3/index.json" Microsoft.dotnet-interactive`

### Start JupyterLab

After the setup is completed you are ready to start working locally with dotenet interactive notebooks. You can run the following command to start up the lab:

```console
jupyter lab
```

This is going to start the lab and put the folder context in whatever path your console or command prompt is in. I tend to store my notebooks in a particular path so you can also use `--notebook-dir=<your path>` to tell JupyterLab to start up in that specific directory. To make this even easier for myself I added the below function to my profile:

```powershell
function jl {
    [cmdletbinding()]
    param ([string]$folder)
    if ([String]::IsNullOrEmpty($folder)) {
        & jupyter lab --notebook-dir=$pwd
    } else {
        & jupyter lab --notebook-dir=$folder
    }
}
```
