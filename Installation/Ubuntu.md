# Gaming on Ubuntu Linux

Ubuntu is a solid system for gaming, so we will create a full gaming OS based on Ubuntu from scratch:

- Install Ubuntu in the disk and finish the setup process. There are no special steps in the setup, just install the OS.
- The installation will require a password to be completed, however, you can remove the password later to activate automated login.
- Once the system has been installed, open the ``Terminal`` application and run the commands below to perform automated gaming setup.

## System Update

Perform a full system update to make sure everything is updated:

```bash
# Update system packages and reboot
sudo apt update
sudo apt upgrade -y
sudo apt dist-upgrade -y
sudo apt autoremove

# Update snap packages
sudo snap refresh

# Reboot
systemctl reboot
```

## Nvidia Drivers

If you are using Nvidia GPUs, you should also install the Nvidia drivers:

```bash
# Nvidia drivers
sudo ubuntu-drivers install
```

## System Optimizations

Remove bloatware:

```bash
# Gnome ONLY
# Remove Gnome bloatware
sudo apt remove -y gnome-tour firefox firefox-*

# Remove snap bloatware
sudo snap remove firefox
```

Install basic packages and media codecs:

```bash
# Add basic packages
sudo apt install -y vim wget curl openssl zip p7zip \
  flatpak-xdg-utils steam-devices android-udev-rules \
  oversteer-udev solaar-udev openrgb-udev-rules

# Enable the Multiverse repository
sudo add-apt-repository multiverse

# Install media codecs
sudo apt install -y ubuntu-restricted-extras
```

Make sure to use Flatpak with FlatHub for better packages:

```bash
# Add flatpak support if not available
if [ ! -x "$(command -v flatpak)" ]; then
    sudo apt install -y flatpak flatpak-xdg-utils
    sudo apt install -y gnome-software gnome-software-plugin-flatpak
fi

# Add FlatHub source
REPOSITORY="https://flathub.org/repo/flathub.flatpakrepo"
flatpak remote-add --if-not-exists flathub $REPOSITORY
flatpak remote-modify --enable flathub
```

## Native Applications

Steam is the only application that I recommend to install natively:

```bash
# Steam & SteamVR
# SteamVR works only with native application
sudo apt install -y steam
```

## Gaming Applications

Now that the system is clean, you can install the desired gaming platform and additional applications. NiceDeck will be used to help with the installation of gaming applications and emulators because it offers additional automation for applications that usually are manually downloaded.

Here is the instructions for usage with Linux:

```bash
# Download executable
REPOSITORY="https://github.com/mateussouzaweb/nicedeck"
sudo wget $REPOSITORY/releases/latest/download/nicedeck-linux-amd64 -O ./nicedeck
sudo chmod +x ./nicedeck

# Self installer
./nicedeck install --programs=nicedeck

# Gaming Stores & Launchers
./nicedeck install --programs=steam
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
# Flatpak extension
# When using Steam flatpak
flatpak install -y flathub com.valvesoftware.Steam.CompatibilityTool.Proton-GE
```

SteamOS session compositing window manager with GameScope:

```bash
# Flatpak extension
# Usage on Steam: gamescope -- %command%
flatpak install -y flathub org.freedesktop.Platform.VulkanLayer.gamescope
```

Vulkan post processing layer to enhance the visual graphics with VkBasalt:

```bash
# Flatpak extension
# Usage on Steam: ENABLE_VKBASALT=1 %command%
flatpak install -y flathub org.freedesktop.Platform.VulkanLayer.vkBasalt
```

## Virtual Reality

NOTE: Only the Steam native application can run SteamVR titles on Linux - flatpak will not work.

```bash
# ALVR - See install instructions at https://github.com/alvr-org/ALVR
```

## Racing Steering Wheel

Oversteer is compatible with many hardware vendors:

```bash
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

Sunshine will works best with native application, so you must manually download the latest .DEB version from website at <https://github.com/LizardByte/Sunshine/releases>. Once downloaded, use the command below to install it:

```bash
sudo apt install -y ./sunshine*.deb
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

Make sure to check out the tweaks section for more specific tips.
That is it, just reboot the system and you are done:

```bash
systemctl reboot
```

Have a good gaming!
