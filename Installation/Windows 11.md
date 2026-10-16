# Gaming on Windows 11

Windows is the most plug and play experience with wider compatibility.

In this setup, we will make sure it uses a local account because it's just better. You can use [Rufus](https://rufus.ie/en/) for an automated process or just follow the basic steps here in the setup process:

- Install Windows 11 Pro on the disk and wait for the setup process initialization. 
- In the setup process, choose "**Set up for work or school**" - this step is VERY IMPORTANT.
- In the next step, do not type the Microsoft account and click in the "**Sign-in options**".
- Select "**Domain join instead**" and type the username for the local account.
- Type a password or leave empty to activate the automated login.
- Finish the Windows setup.

Once the Windows has been installed, please make sure to activate the Windows license and install all the necessary drivers for your hardware: 

- AMD drivers: <https://www.amd.com/en/support/download/drivers.html>
- Nvidia drivers: <https://www.nvidia.com/en-us/drivers>
- Intel drivers: <https://www.intel.com/content/www/us/en/download-center/home.html>

When the basic system setup has been finished, open the ``Terminal`` application and run the commands below to perform automated gaming setup.

## Basic Operations

The process include commands to remove system bloatware, install basic packages and perform system upgrades:

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

Now that the system is clean, you can install the desired gaming platform and additional applications. NiceDeck will be used to help with the installation of gaming applications and emulators because it offers additional automation for applications that usually are manually downloaded.

Here is the instructions for usage with Windows:

```bash
# Download executable
cd "$env:USERPROFILE\Downloads"
$REPOSITORY="https://github.com/mateussouzaweb/nicedeck"
wget $REPOSITORY/releases/latest/download/nicedeck-windows-cli-amd64.exe -OutFile nicedeck.exe

# Self installer
.\nicedeck.exe install-programs --programs=nicedeck

# Gaming Stores & Launchers
.\nicedeck.exe install-programs --programs=steam
.\nicedeck.exe install-programs --programs=epic-games
.\nicedeck.exe install-programs --programs=ea-app
.\nicedeck.exe install-programs --programs=ubisoft-connect
.\nicedeck.exe install-programs --programs=gog-galaxy
.\nicedeck.exe install-programs --programs=amazon-games
.\nicedeck.exe install-programs --programs=battle-net
.\nicedeck.exe install-programs --programs=rockstar-games-launcher
.\nicedeck.exe install-programs --programs=heroic-games
.\nicedeck.exe install-programs --programs=es-de

# Others
.\nicedeck.exe install-programs --programs=discord

# Streaming
.\nicedeck.exe install-programs --programs=moonlight
.\nicedeck.exe install-programs --programs=chiaki-ng
.\nicedeck.exe install-programs --programs=geforce-now
.\nicedeck.exe install-programs --programs=xbox-cloud-gaming

# Browsers
.\nicedeck.exe install-programs --programs=brave-browser
.\nicedeck.exe install-programs --programs=google-chrome
.\nicedeck.exe install-programs --programs=microsoft-edge
.\nicedeck.exe install-programs --programs=firefox

# Emulators
.\nicedeck.exe install-programs --programs=cemu
.\nicedeck.exe install-programs --programs=eden
.\nicedeck.exe install-programs --programs=pcsx2
.\nicedeck.exe install-programs --programs=rpcs3
.\nicedeck.exe install-programs --programs=ryujinx
.\nicedeck.exe install-programs --programs=shadps4
.\nicedeck.exe install-programs --programs=xenia

.\nicedeck.exe install-programs --programs=azahar
.\nicedeck.exe install-programs --programs=dolphin
.\nicedeck.exe install-programs --programs=duckstation
.\nicedeck.exe install-programs --programs=flycast
.\nicedeck.exe install-programs --programs=melonds
.\nicedeck.exe install-programs --programs=mgba
.\nicedeck.exe install-programs --programs=ppsspp
.\nicedeck.exe install-programs --programs=redream
.\nicedeck.exe install-programs --programs=gopher64
.\nicedeck.exe install-programs --programs=vita3k
.\nicedeck.exe install-programs --programs=xemu

# Remove temporary copy after installation 
rm .\nicedeck.exe
```

Additional applications for specific use cases are available in the next topics.

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

## Finishing Setup 

Make sure to check out the tweaks section for more specific tips.
That is it, just reboot the system and you are done.

Have a good gaming!
