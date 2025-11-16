# Gaming on Fedora Linux

Fedora is a pretty capable system for gaming, so we will create a full gaming OS based on Fedora from scratch:

- You can choose to install **Fedora Workstation** or **Fedora KDE** and it should work for others desktop environments as well that are provided by Fedora, just pick the best for you.
- Install Fedora in the disk and finish the setup process. There are no special steps in the setup, just install Fedora.
- The installation will require a password to be completed, however, you can remove the password later to activate automated login.

If you are using Nvidia GPUs, you should also install the Nvidia drivers after finishing installation:

```bash
# Nvidia drivers
sudo dnf install -y akmod-nvidia
```

Once the system has been installed, open the ``Terminal`` (Gnome) or ``Konsole`` (KDE) application and run the commands below to perform automated gaming setup.

## Basic Operations

Here are the relevant commands to remove bloatware, install basic packages and perform system upgrades:

```bash
# KDE ONLY
# Remove KDE bloatware
sudo dnf remove -y kamoso kpat kmines kaddressbook \
  kcharselect kmouth kdebugsettings kmousetool krfb \
  kfind kmahjongg kolourpaint skanpage mediawriter neochat \
  akregator krdc plasma-welcome akonadiimportwizard qrca \
  kde-connect kde-connect-* kmail kmail-* kontact kontact-* \
  korganizer korganizer-* libreoffice libreoffice-* firefox firefox-*

# Gnome ONLY
# Remove Gnome bloatware
sudo dnf remove -y gnome-tour firefox firefox-*

# Add basic packages
sudo dnf install -y vim wget curl openssl zip p7zip \
  flatpak-xdg-utils steam-devices android-udev-rules \
  oversteer-udev solaar-udev openrgb-udev-rules

# Update system packages
sudo dnf update -y
```

Better media codecs (please use the commands based on your graphics card):

```bash
# Install media codecs with RPM-Fusion
# https://rpmfusion.org/Howto/Multimedia
sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1
sudo dnf swap -y ffmpeg-free ffmpeg --allowerasing
sudo dnf install -y ffmpeg-libs libva libva-utils

# Codecs for AMD
sudo dnf swap -y mesa-va-drivers mesa-va-drivers-freeworld
sudo dnf swap -y mesa-vdpau-drivers mesa-vdpau-drivers-freeworld
sudo dnf swap -y mesa-va-drivers.i686 mesa-va-drivers-freeworld.i686
sudo dnf swap -y mesa-vdpau-drivers.i686 mesa-vdpau-drivers-freeworld.i686

# Codecs for Nvidia
sudo dnf install -y libva-nvidia-driver
sudo dnf install -y libva-nvidia-driver.i686
sudo dnf install -y libva-nvidia-driver.x86_64

# Codecs for Intel
sudo dnf install -y intel-media-driver
```

## System Optimizations

Makes startup boot significantly faster by disabling network await:

```bash
# Disable network wait online
# This makes startup boot significantly faster
sudo systemctl disable NetworkManager-wait-online
```

Make sure to use Flatpak with FlatHub for better packages:

```bash
# Add FlatHub source
REPOSITORY="https://flathub.org/repo/flathub.flatpakrepo"
flatpak remote-add --if-not-exists flathub $REPOSITORY
flatpak remote-modify --enable flathub

# Remove KDE bloatware
flatpak remove -y org.kde.kmines
flatpak remove -y org.kde.krdc
flatpak remove -y org.kde.kolourpaint
flatpak remove -y org.kde.elisa
flatpak remove -y org.kde.kmahjongg
flatpak remove -y org.kde.skanpage

# Remove Gnome bloatware
flatpak remove -y org.fedoraproject.MediaWriter
flatpak remove -y org.gnome.Contacts
flatpak remove -y org.gnome.Snapshot
flatpak remove -y org.gnome.Maps

# Reinstall apps from FlatHub and update everything else
REINSTALL=$(flatpak list --columns=application | grep -v fedora)
flatpak install -y --reinstall flathub $(echo $REINSTALL)
flatpak update -y

# Remove Fedora repository
flatpak remote-delete fedora
```

## Native Applications

You will find the native game applications here, but Steam is the only application that I recommend to install natively:

```bash
# Steam & SteamVR
# SteamVR works only with native application
sudo dnf install -y steam

# Heroic Games Launcher 
sudo dnf copr enable -y atim/heroic-games-launcher
sudo dnf install -y heroic-games-launcher-bin

# Lutris
sudo dnf install -y lutris
```

## Gaming Applications

Now that the system is clean, you can install the desired gaming platform and additional applications. NiceDeck will be used to help with the installation of gaming applications and emulators because it offers additional automation for applications that usually are manually downloaded.

Here is the instructions for usage with Linux:

```bash
# Download executable
REPOSITORY="https://github.com/mateussouzaweb/nicedeck/releases/download"
sudo wget $REPOSITORY/v0.2.4/nicedeck-linux-amd64 -O ./nicedeck
sudo chmod +x ./nicedeck

# Self installer
./nicedeck install --programs=nicedeck

# Steam
# NOTE: You should install Steam and log in with your account into Steam first 
./nicedeck install --programs=steam

# Gaming Stores & Launchers
./nicedeck install --programs=epic-games
./nicedeck install --programs=ea-app
./nicedeck install --programs=ubisoft-connect
./nicedeck install --programs=gog-galaxy
./nicedeck install --programs=amazon-games
./nicedeck install --programs=battle-net

# Alternative Launchers
./nicedeck install --programs=heroic-games
./nicedeck install --programs=lutris
./nicedeck install --programs=bottles
./nicedeck install --programs=es-de

# Others
./nicedeck install --programs=discord
./nicedeck install --programs=proton-plus

# Streaming
./nicedeck install --programs=moonlight
./nicedeck install --programs=chiaki-ng
./nicedeck install --programs=geforce-now
./nicedeck install --programs=xbox-cloud-gaming

# Browsers
./nicedeck install --programs=brave-browser
./nicedeck install --programs=google-chrome
./nicedeck install --programs=microsoft-edge
./nicedeck install --programs=firefox

# Emulators
./nicedeck install --programs=cemu
./nicedeck install --programs=citron
./nicedeck install --programs=eden
./nicedeck install --programs=pcsx2
./nicedeck install --programs=rpcs3
./nicedeck install --programs=ryujinx
./nicedeck install --programs=shadps4
./nicedeck install --programs=xenia

./nicedeck install --programs=azahar
./nicedeck install --programs=dolphin
./nicedeck install --programs=duckstation
./nicedeck install --programs=flycast
./nicedeck install --programs=melonds
./nicedeck install --programs=mgba
./nicedeck install --programs=ppsspp
./nicedeck install --programs=redream
./nicedeck install --programs=simple64
./nicedeck install --programs=vita3k
./nicedeck install --programs=xemu
```

Additional applications for specific use cases are available in the next topics.

## In Game Utilities

Proton GE compatibility layer for non Steam games and applications:

```bash
# When using Steam flatpak
flatpak install -y flathub com.valvesoftware.Steam.CompatibilityTool.Proton-GE
```

SteamOS session compositing window manager with GameScope:

```bash
# Usage on Steam: gamescope -- %command%
sudo dnf install -y gamescope

# Flatpak extension
flatpak install -y flathub org.freedesktop.Platform.VulkanLayer.gamescope
```

Vulkan post processing layer to enhance the visual graphics with VkBasalt:

```bash
# Usage on Steam: ENABLE_VKBASALT=1 %command%
sudo dnf install -y vkBasalt

# Flatpak extension
flatpak install -y flathub org.freedesktop.Platform.VulkanLayer.vkBasalt
```

## Virtual Reality

NOTE: Only the Steam native application can run SteamVR titles on Linux - flatpak will not work.

```bash
# ALVR - See instructions for usage on Steam: https://github.com/alvr-org/ALVR
sudo dnf copr enable -y grillo-delmal/alvr
sudo dnf install -y alvr
```

## Racing Steering Wheel

Oversteer is compatible with many hardware vendors:

```bash
# Oversteer
sudo dnf copr enable -y peem/oversteer
sudo dnf install -y oversteer python3-evdev

# Flatpak version 
flatpak install -y flathub io.github.berarma.Oversteer

# Flatpak permissions
DESTINATION="/usr/lib/udev/rules.d/"
REPOSITORY="https://github.com/berarma/oversteer/raw/refs/heads/master/data/udev"
sudo wget $REPOSITORY/99-fanatec-wheel-perms.rules -P $DESTINATION
sudo wget $REPOSITORY/99-logitech-wheel-perms.rules -P $DESTINATION
sudo wget $REPOSITORY/99-thrustmaster-wheel-perms.rules -P $DESTINATION
sudo udevadm control --reload-rules && sudo udevadm trigger
```

Additional commands for specific hardware support:

```bash
# Support for Logitech G923 
# (connect the USB cable then run the command)
sudo usb_modeswitch -v 046d -p c26d -M 0f00010142 -C 0x03 -m 01 -r 01
```

## Remote Streaming

Sunshine is a solid application for streaming and remote gaming and will works best with their native application:

```bash
# Sunshine
sudo dnf copr enable -y lizardbyte/beta
sudo dnf install -y Sunshine
```

## Others Tools

Useful applications recommended for your gaming OS:

```bash
# Ignition (configure startup applications)
flatpak install -y flathub io.github.flattool.Ignition

# Mission Center (system task manager)
flatpak install -y flathub io.missioncenter.MissionCenter
```

## Finishing Setup 

That is it, just reboot the system and you are done:

```bash
systemctl reboot
```

Linux is always improving on gaming, but please be aware that most online games does not work due to anti-cheat programs.

Have a good gaming!
