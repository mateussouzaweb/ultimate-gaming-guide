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
# https://github.com/mateussouzaweb/nicedeck
cd "$env:USERPROFILE\Downloads"
$REPOSITORY="https://github.com/mateussouzaweb/nicedeck/releases/download"
wget $REPOSITORY/v0.2.4/nicedeck-windows-cli-amd64.exe -OutFile nicedeck.exe

# Self installer
.\nicedeck.exe install --programs=nicedeck

# Steam
# NOTE: Is recommended to install Steam and log in with your account first
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
.\nicedeck.exe install --programs=citron
.\nicedeck.exe install --programs=eden
.\nicedeck.exe install --programs=pcsx2
.\nicedeck.exe install --programs=rpcs3
.\nicedeck.exe install --programs=ryujinx
.\nicedeck.exe install --programs=shadps4
.\nicedeck.exe install --programs=xenia

.\nicedeck.exe install --programs=azahar
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

## Windows Performance Tips

- Make sure to install the latest chipset and GPU driver in the system.
- Set [Power Plan to High Performance](https://help.ableton.com/hc/en-us/articles/115000211304-Using-the-High-performance-power-plan-Windows-) in Control Panel.
- Disable [Fast Startup](https://pureinfotech.com/disable-fast-startup-windows-11-10/) in the Power Options.
- Disable [Xbox Game Bar](https://apps.microsoft.com/store/detail/9NZKPSTSNW4P?hl=pt-br&gl=BR) in Windows Settings.
- Disable [Game Mode](https://support.xbox.com/en-US/help/games-apps/game-setup-and-play/use-game-mode-gaming-on-pc) in Windows Settings (yes, disable).
- Enable [Variable Refresh Rate](https://www.elevenforum.com/t/enable-or-disable-variable-refresh-rate-for-games-in-windows-11.12052/) (VRR) in Graphics Settings.
- Enable [Optimizations for Windowed Games](https://support.microsoft.com/en-us/windows/optimizations-for-windowed-games-in-windows-11-3f006843-2c7e-4ed0-9a5e-f9389e535952) in Graphics Settings.
- On AMD GPUs, enable [Smart Access Memory](https://www.amd.com/en/technologies/smart-access-memory) on BIOS and AMD Software.

## Windows Design Tweaks

- Open "Settings" application.
- Go to "Personalization" > "Colors" and set color mode as "Dark".
- Go to "Personalization" > "Start" and tweak the settings based on you preferences.
- Go to "Personalization" > "Taskbar" and tweak the settings based on you preferences.
- Go to "System" > "Multitasking" > and change the Alt+Tab experience to not show/include Microsoft Edge tabs.

## Windows Automatic Login

Disabling password requirement for login is pretty easy. If you want to disable password, there a few required settings to enable automatic login on Windows:

- Open "Settings" application.
- Go to "Accounts" > "Sign-in Options".
- Disable the "For improved security, only allow Windows Hello sign-in for Microsoft accounts on this device" option.
- Disable the "Use my sign-in info to automatically finish setting up after an update" option.
- Set "If you've been away, when should Windows require you to sign in again?" as "Never" to avoid typing passwords when computer wake up from sleep.
- In the "Dynamic lock" section, uncheck the available option.
- Disable all "Windows Hello" options to use only the password option.

Now, to remove the account password, follow the steps below:

- In the "Password" option, click on "Change" button.
- Type the current password and click on "Next" button.
- Leave the new password fields empty and click "Next".
- Finally, click on "Finish" to complete the process.

Restart the system and see that the automatic login feature is working.

## Finishing Setup 

That is it, just reboot the system and you are done.

Have a good gaming!
