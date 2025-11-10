# Gaming on Windows 11

Windows is the most plug and play experience with wider compatibility.

In this setup, we will make sure it uses a local account because it's just better:

- Install Windows in the disk and wait for the setup process initialization.
- In the setup process, choose "**Set up for work or school**" - this step is VERY IMPORTANT.
- In the next step, do not type the Microsoft account and click in the "**Sign-in options**".
- Select "**Domain join instead**" and type the username for the local account.
- Type a password or leave empty to activate the automated login.
- Finish the Windows setup.

Once the Windows has been installed, please make sure to install all the necessary drivers for your hardware: 

- AMD drivers: <https://www.amd.com/en/support/download/drivers.html>
- Nvidia drivers: <https://www.nvidia.com/en-us/drivers>
- Intel drivers: <https://www.intel.com/content/www/us/en/download-center/home.html>

When the basic system setup has been finished, open the ``Terminal`` application and run the commands below to perform automated gaming setup.

## Basic Operations

Process include commands to remove system bloatware, install basic packages and perform system upgrades:

```bash
# Remove bloatware
winget uninstall -q "Copilot"
winget uninstall -q "Microsoft Teams"
winget uninstall -q "Microsoft Clipchamp"
winget uninstall -q "Microsoft News"
winget uninstall -q "Microsoft Bing"
winget uninstall -q "Microsoft Edge Game Assist"
winget uninstall -q "Microsoft 365 (Office)"
winget uninstall -q "Solitaire & Casual Games"
winget uninstall -q "Microsoft Sticky Notes"
winget uninstall -q "Outlook for Windows"
winget uninstall -q "Paint"
winget uninstall -q "Microsoft To Do"
winget uninstall -q "Windows Camera"
winget uninstall -q "Feedback Hub"
winget uninstall -q "Phone Link"
winget uninstall -q "Microsoft OneDrive"
winget uninstall -q "MSN Weather"
winget uninstall -q "Dev Home"
winget uninstall -q "Game Speech Window"
winget uninstall -q "Quick Assist"
winget uninstall -q "Get Help"

# Add basic packages
winget install -e --id Microsoft.DotNet.Runtime.8
winget install -e --id Microsoft.VCRedist.2015+.x64
winget install -e --id 7zip.7zip

# Upgrade system packages
winget upgrade --all --include-unknown
```

## Gaming Applications

NiceDeck will be used to help with the installation of gaming applications and emulators.

Here is the instructions for usage with Windows:

```bash
# Download executable
# https://github.com/mateussouzaweb/nicedeck
cd "$env:USERPROFILE\Downloads"
$REPOSITORY="https://github.com/mateussouzaweb/nicedeck/releases/download"
wget $REPOSITORY/v0.2.4/nicedeck-windows-cli-amd64.exe -OutFile nicedeck.exe

# Self installer
.\nicedeck.exe install --programs=nicedeck

# Steam
# NOTE: You should install Steam and log in with your account into Steam first 
.\nicedeck.exe install --programs=steam

# Gaming Stores & Launchers
.\nicedeck.exe install --programs=epic-games
.\nicedeck.exe install --programs=ea-app
.\nicedeck.exe install --programs=ubisoft-connect
.\nicedeck.exe install --programs=gog-galaxy
.\nicedeck.exe install --programs=amazon-games
.\nicedeck.exe install --programs=battle-net

# Alternative Launchers
.\nicedeck.exe install --programs=heroic-games
.\nicedeck.exe install --programs=es-de

# Others
.\nicedeck.exe install --programs=discord

# Streaming
.\nicedeck.exe install --programs=moonlight
.\nicedeck.exe install --programs=chiaki-ng
.\nicedeck.exe install --programs=geforce-now
.\nicedeck.exe install --programs=xbox-cloud-gaming

# Browsers
.\nicedeck.exe install --programs=brave-browser
.\nicedeck.exe install --programs=google-chrome
.\nicedeck.exe install --programs=microsoft-edge
.\nicedeck.exe install --programs=firefox

# Emulators
.\nicedeck.exe install --programs=cemu
.\nicedeck.exe install --programs=eden
.\nicedeck.exe install --programs=pcsx2
.\nicedeck.exe install --programs=rpcs3
.\nicedeck.exe install --programs=ryujinx
.\nicedeck.exe install --programs=shadps4
.\nicedeck.exe install --programs=xenia

.\nicedeck.exe install --programs=azahar
.\nicedeck.exe install --programs=citron
.\nicedeck.exe install --programs=dolphin
.\nicedeck.exe install --programs=duckstation
.\nicedeck.exe install --programs=flycast
.\nicedeck.exe install --programs=melonds
.\nicedeck.exe install --programs=mgba
.\nicedeck.exe install --programs=ppsspp
.\nicedeck.exe install --programs=redream
.\nicedeck.exe install --programs=simple64
.\nicedeck.exe install --programs=vita3k
.\nicedeck.exe install --programs=xemu
```

## Library Manager

Universal library manager for everything if you don't want to use Steam:

```bash
winget install -e --id Playnite.Playnite
```

## Virtual Reality

I recommend using only Steam VR and Virtual Desktop for VR gaming. You don't need any additional software:

```bash
winget install -e --id VirtualDesktop.Streamer
```

## Racing Steering Wheel

Software is based on your hardware:

```bash
winget install -e --id Logitech.GHUB
```

## Remote Streaming

Sunshine is a solid application for streaming and remote gaming, however I recommend trying Apollo on Windows due its advanced features:

```bash
# Recommended
winget install -e --id ClassicOldSong.Apollo

# Alternative
winget install -e --id LizardByte.Sunshine
```

## Windows Tweaks

- Open "Settings" application.
- Go to "Personalization" > "Colors" and set "Dark".
- Go to "Personalization" > "Start" and tweak the settings based on you preferences.
- Go to "Personalization" > "Taskbar" and tweak the settings based on you preferences.
- Go to "System" > "Multitasking" > and change the Alt+Tab experience to now show Microsoft Edge tabs.

## Windows Automatic Login

First, there a few required settings to automatic login works if you set up Windows with passwords:

- Open "Settings".
- Go to "Accounts" > "Sign in Options".
- Disable all "Windows Hello" ways to sign in options.
- Disable the "For improved security, only allow Windows Hello sign-in for Microsoft accounts on this device" option.
- Disable the "Use my sign-in info to automatically finish setting up after an update" option.
- Set "If you've been away, when should Windows require you to sign in again?" as "Never" to avoid typing passwords when computer wake up from sleep.
- In the "Dynamic lock" section, uncheck the available option.

On the requirements are meet, you can disable password requirement with the Microsoft provided solution:

```bash
# Install
winget install --id=Sysinternals.Autologon  -e

# Open new terminal tab and execute the program
# In the GUI, type account password and click "Enable"
AutoLogon64.exe
```

Restart the system and see that the automatic login feature is working.

## Finishing Setup 

That is it, just reboot the system and you are done.

Have a good gaming!
