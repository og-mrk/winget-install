![winget Windows 10](https://github.com/asheroto/winget-install/assets/49938263/49594040-88ff-43f3-b3da-a8db5fd997d6)

[![PowerShell Gallery Downloads](https://img.shields.io/powershellgallery/dt/winget-install?label=PowerShell%20Gallery%20downloads)](https://www.powershellgallery.com/packages/winget-install)
[![GitHub Downloads - All Releases](https://img.shields.io/github/downloads/asheroto/winget-install/total?label=release%20downloads)](https://github.com/asheroto/winget-install/releases)
[![Release](https://img.shields.io/github/v/release/asheroto/winget-install)](https://github.com/asheroto/winget-install/releases)
[![GitHub Release Date - Published_At](https://img.shields.io/github/release-date/asheroto/winget-install)](https://github.com/asheroto/winget-install/releases)

[![GitHub Sponsor](https://img.shields.io/github/sponsors/asheroto?label=Sponsor&logo=GitHub)](https://github.com/sponsors/asheroto?frequency=one-time&sponsor=asheroto)
<a href="https://ko-fi.com/asheroto"><img src="https://ko-fi.com/img/githubbutton_sm.svg" alt="Ko-Fi Button" height="20px"></a>
<a href="https://www.buymeacoffee.com/asheroto"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=seb6596&button_colour=FFDD00&font_colour=000000&font_family=Lato&outline_colour=000000&coffee_colour=ffffff](https://img.buymeacoffee.com/button-api/?text=Buy%20me%20a%20coffee&emoji=&slug=asheroto&button_colour=FFDD00&font_colour=000000&font_family=Lato&outline_colour=000000&coffee_colour=ffffff)" height="40px"></a>

# Install winget from PowerShell

**winget, a command line package manager, doesn't have a command line installer? 🤣 Now it does! 😊**

> [!NOTE]
> Microsoft released some new short URLs that work well for installing winget. This is the new script that is smaller and faster at installing winget!

## Requirements

-   Requires PowerShell running with Administrator rights
-   Compatible with:
    -   Windows 10 (Version 1809 or higher)
    -   Windows 11
    -   Server 2022
    -   Windows Sandbox
-   Not compatible with:
    -   Server 2019 (winget not supported)

## Features

-   Installs [winget-cli](https://github.com/microsoft/winget-cli) directly from PowerShell
-   Always fetches the latest `winget` version
-   Automatically verifies OS compatibility
-   Determines and installs the appropriate prerequisites based on OS version
-   Supports x86/x64 and arm/arm64 architectures
-   Allows bypassing of existing `winget` installation verification through `-Force` parameter or `$Force` session variable
-   Supports irm/iex one-line command using short URL
-   Supports automatically relaunching in conhost and ending active processes associated with winget that could interfere with the installation
-   Code is hosted on [PowerShell Gallery](https://www.powershellgallery.com/packages/winget-install)

## Script Functionality

-   Identifies processor architecture to decide which prerequisites are needed (x86/x64 or arm/arm64)
-   Checks Windows OS version for compatibility (Windows 10, Windows 11, Server 2022)
-   Verifies Windows 10 release ID for compatibility (must be 1809 or newer)
-   Uses the UI.Xaml and VCLibs as [recommended by Microsoft](https://learn.microsoft.com/en-us/windows/package-manager/winget/#install-winget-on-windows-sandbox)
-   The winget-cli license is downloaded using the latest version from GitHub
-   [winget-cli](https://github.com/microsoft/winget-cli) is then installed using the latest version from GitHub
-   Runs command registration if the `winget` command is not detected at the end of installation

## Setup

### Method 1 - PowerShell Gallery

> [!TIP]
>If you want to trust PSGallery so you aren't prompted each time you run this command, or if you're scripting this and want to ensure the script isn't interrupted the first time it runs...
>```powershell
>Install-PackageProvider -Name "NuGet" -Force
>Set-PSRepository -Name "PSGallery" -InstallationPolicy Trusted
>```

**This is the recommended method, because it always gets the public release that has been tested, it's easy to remember, and supports all parameters.**

Open PowerShell as Administrator and type

```powershell
Install-Script winget-install -Force
```

Follow the prompts to complete the installation (you can tap `A` to accept all prompts or `Y` to select them individually.

**Note:** `-Force` is optional but recommended, as it will force the script to update if it is outdated. If you do not use `-Force`, it will _not_ overwrite the script if outdated.

#### Usage

```powershell
winget-install
```

If `winget` is already installed, you can use the `-Force` parameter to force the script to run anyway.

The script is published on [PowerShell Gallery](https://www.powershellgallery.com/packages/winget-install) under `winget-install`.

### Method 2 - One Line Command (Runs Immediately)

The URL [asheroto.com/winget](https://asheroto.com/winget) always redirects to the [latest code-signed release](https://github.com/asheroto/winget-install/releases/latest/download/winget-install.ps1) of the script.

If you just need to run the basic script without any parameters, you can use the following one-line command:

#### Option A:

```powershell
irm asheroto.com/winget | iex
```

Due to the nature of how PowerShell works, you won't be able to use any parameters like `-Force` with this command line. You can set the global variable `$Force` to `$true` and the script should pick up on it ([more info](#global-variables)), but if for some reason that doesn't work or you absolutely need to use a one-line command with parameters, you can use the following:

```powershell
&([ScriptBlock]::Create((irm asheroto.com/winget))) -Force
```

#### Option B:

To make it easier to remember, you can also use the URL [winget.pro](https://winget.pro) which redirects to the same URL. This URL is provided courtesy of [Omaha Consulting](https://github.com/omaha-consulting).

```powershell
irm winget.pro | iex
```

Due to the nature of how PowerShell works, you won't be able to use any parameters like `-Force` with this command line. You can set the global variable `$Force` to `$true` and the script should pick up on it ([more info](#global-variables)), but if for some reason that doesn't work or you absolutely need to use a one-line command with parameters, you can use the following:

```powershell
&([ScriptBlock]::Create((irm winget.pro))) -Force
```

#### Option C:

Alternatively, you can of course use the latest code-signed release URL directly:

```powershell
irm https://github.com/asheroto/winget-install/releases/latest/download/winget-install.ps1 | iex
```

### Method 3 - Download Locally and Run

As a more conventional approach, download the latest [winget-install.ps1](https://github.com/asheroto/winget-install/releases/latest/download/winget-install.ps1) from [Releases](https://github.com/asheroto/winget-install/releases), then run the script as follows:

```powershell
.\winget-install.ps1
```

You can use the `-Force` or `-ForceClose` parameters if needed, or use `$Force = $true` and `$ForceClose = $true` global session variables if preferred.

> [!TIP]
> If for some reason your PowerShell window closes at the end of the script and you don't want it to, or don't want your other scripts to be interrupted, you can wrap the command in a `powershell "COMMAND HERE"`. For example, `powershell "irm asheroto.com/winget | iex"`.

## Parameters

**No parameters are required** to run the script, but there are some optional parameters to use if needed.

| Parameter         | Description                                                                                                                                                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-Debug`          | Enables debug mode, which shows additional information for debugging.                                                                                                                                                                                  |
| `-Force`          | Ensures installation of winget and its dependencies, even if already present.                                                                                                                                                                          |
| `-ForceClose`     | Windows Terminal sometimes has trouble installing winget; run the script with the -ForceClose parameter to relaunch the script in conhost.exe and automatically end active processes associated with winget that could interfere with the installation |
| `-CheckForUpdate` | Checks if there is an update available for the script.                                                                                                                                                                                                 |
| `-Wait`           | By default, the script will exit immediately after completion. If you need some time to observe the script output, you can use this parameter to force the script to pause for several seconds before exiting.                                         |
| `-UpdateSelf`     | Updates the script to the latest version.                                                                                                                                                                                                              |
| `-Version`        | Displays the version of the script.                                                                                                                                                                                                                    |
| `-Help`           | Displays the full help information for the script.                                                                                                                                                                                                     |

### Example Parameters Usage

```powershell
winget-install -Force
```

## Global Variables

Global variables are _optional_ and are only needed if you don't want to use parameters. They can be set before running the script, or you can set them in your PowerShell profile to always use them.

| Variable      | Description                                                                                                                                                                                                                                            |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `$Debug`      | Enables debug mode, which shows additional information for debugging.                                                                                                                                                                                  |
| `$Force`      | Ensures installation of winget and its dependencies, even if already present.                                                                                                                                                                          |
| `$ForceClose` | Windows Terminal sometimes has trouble installing winget; run the script with the -ForceClose parameter to relaunch the script in conhost.exe and automatically end active processes associated with winget that could interfere with the installation |

### Example Global Variables Usage

```powershell
$Force = $true
winget-install
```

## Troubleshooting

-   Before releasing a new version, the script is tested on a clean install of Windows 10 22H2, Server 2022 21H2, and Windows 11 22H2
-   If you run into an issue, please ensure your system is compatible & fully updated
-   Sometimes PowerShell accidentally closes the window before you can read the output, so you can use the `-Wait` parameter to pause the script for a few seconds before exiting if this is happening on your system
-   Try running `winget-install` again, sometimes the script will fail due to a temporary issue with the prerequisite server URLs
-   Try using the `-Debug` parameters to see if it provides any additional information
-   If you're getting a `resource in use` error message, run the script again with the `-ForceClose` parameter
-   Try [installing winget manually](https://github.com/microsoft/winget-cli#manually-update) to see if the issue exists with winget itself
-   If the issue occurs when installing winget manually, please open an [issue on the winget-cli repo](https://github.com/microsoft/winget-cli/issues) (unrelated to this script)
-   Check the [winget-cli Troubleshooting Guide](https://github.com/microsoft/winget-cli/blob/master/doc/troubleshooting/README.md)
-   If the problem **only** occurs when using this script, please open an issue here

## Contributing

If you'd like to help develop this project: fork the repo, edit the code, then submit a pull request. 😊