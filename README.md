# 🎂 Python Poetry Installer (for Windows) 🎂

> **Anniversary Edition** Celebrating the first-year anniversary of [this](https://github.com/python-poetry/install.python-poetry.org/issues/112) issue. [🖖](https://en.wikipedia.org/wiki/Vulcan_salute)

This repository is a clone of [Poetry's official installation script](https://github.com/python-poetry/install.python-poetry.org) modified to work on Windows because of Python SSL certificates hell.

It disables SSL certificates validation.

**THIS IS UNSAFE. DO NOT USE THIS. YOU HAVE BEEN WARNED.**

## Usage

### Windows powershell

```powershell
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/fdcastel/install-poetry/main/install-poetry.py -UseBasicParsing).Content | py -
```

You will probably want to run this, too (to fix your `PATH` environment variable):

```powershell
# Source: https://stackoverflow.com/a/34844707
function Add-EnvPath {
    param(
        [Parameter(Mandatory=$true)]
        [string] $Path,

        [ValidateSet('Machine', 'User', 'Session')]
        [string] $Container = 'Session'
    )

    if ($Container -ne 'Session') {
        $containerMapping = @{
            Machine = [EnvironmentVariableTarget]::Machine
            User = [EnvironmentVariableTarget]::User
        }
        $containerType = $containerMapping[$Container]

        $persistedPaths = [Environment]::GetEnvironmentVariable('Path', $containerType) -split ';'
        if ($persistedPaths -notcontains $Path) {
            $persistedPaths = $persistedPaths + $Path | where { $_ }
            [Environment]::SetEnvironmentVariable('Path', $persistedPaths -join ';', $containerType)
        }
    }

    $envPaths = $env:Path -split ';'
    if ($envPaths -notcontains $Path) {
        $envPaths = $envPaths + $Path | where { $_ }
        $env:Path = $envPaths -join ';'
    }
}

function Reload-Path {
    # Updates current session PATH reading the most updated one from Registry
    $env:Path =  (Get-ItemProperty 'HKLM:\System\CurrentControlSet\Control\Session Manager\Environment').Path + ';' + `
                 (Get-ItemProperty 'HKCU:\Environment').Path
}

Add-EnvPath -Path "$env:APPDATA\Python\Scripts" -Container User
Reload-Path
```
