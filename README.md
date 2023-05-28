# Python Poetry Installer (for Windows)

This repository is a clone of [Poetry's official installation script](https://github.com/python-poetry/install.python-poetry.org) modified to work on Windows because of Python SSL certificates hell.

It disables SSL certificates validation.

**THIS IS UNSAFE. DO NOT USE THIS. YOU HAVE BEEN WARNED.**

## Usage

### Windows powershell

```powershell
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/fdcastel/install-poetry/main/install-poetry.py -UseBasicParsing).Content | py -
```

