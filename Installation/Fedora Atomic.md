# Gaming on Fedora Atomic Linux

Fedora is a pretty capable system for gaming, and offers immutable OS options in Atomic Desktop formats. We will create a full gaming OS based on Fedora from scratch:

- You can choose to install **Fedora Silverblue** or **Fedora Kinoite** and it should work for others desktop environments as well that are provided by Fedora in Atomic Desktop format.
- Install Fedora in the disk and finish the setup process. There are no special steps in the setup, just install Fedora.
- The installation will require a password to be completed, however, you can remove the password later to activate automated login.

If you are using Nvidia GPUs, you should also install the Nvidia drivers after finishing installation:

```bash
# Add RPM-Fusion
# https://rpmfusion.org/Howto/OSTree
rpm-ostree install -y \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Nvidia drivers
# https://rpmfusion.org/Howto/NVIDIA
rpm-ostree install -y akmod-nvidia
rpm-ostree kargs \
  --append-if-missing="rd.driver.blacklist=nouveau" \
  --append-if-missing="modprobe.blacklist=nouveau"
```

Once the system has been installed, open the ``Terminal`` (Gnome) or ``Konsole`` (KDE) application and run the commands below to perform automated gaming setup.

## Basic Operations

Here are the steps to perform if you are using immutable OS to remove bloatware, install basic packages and perform system upgrades:

```bash
# Update system and reboot
rpm-ostree update
systemctl reboot

# KDE ONLY
# Remove KDE bloatware
rpm-ostree override remove \
  kdebugsettings krfb krfb-* kdeconnectd \
  kde-connect kde-connect-* firefox firefox-*

# GNOME ONLY
# Remove Gnome bloatware
rpm-ostree override remove gnome-tour firefox firefox-*

# Add basic packages
rpm-ostree install -y p7zip flatpak-xdg-utils steam-devices
```

Better media codecs (please use the commands based on your graphics card):

```bash
# Add RPM-Fusion (skip if already installed)
# https://rpmfusion.org/Howto/OSTree
rpm-ostree install -y \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Install media codecs with RPM-Fusion
# https://rpmfusion.org/Howto/OSTree
rpm-ostree override remove ffmpeg-free libavcodec-free libavdevice-free \
  libavfilter-free libavformat-free libavutil-free \
  libpostproc-free libswresample-free libswscale-free \
  --install=ffmpeg \
  --install=ffmpeg-libs \
  --install=libva-utils \
  --install=vdpauinfo \
  --install=gstreamer1-plugins-bad-free-extras \
  --install=gstreamer1-plugins-bad-freeworld \
  --install=gstreamer1-plugins-ugly \
  --install=gstreamer1-vaapi

# Codecs for AMD
rpm-ostree override remove mesa-va-drivers mesa-vdpau-drivers \
  mesa-va-drivers.i686 mesa-vdpau-drivers.i686 \
  --install=mesa-va-drivers-freeworld \
  --install=mesa-vdpau-drivers-freeworld \
  --install=mesa-vdpau-drivers-freeworld.i686 \
  --install=mesa-vdpau-drivers-freeworld.i686

# Codecs for Nvidia
rpm-ostree install -y libva-nvidia-driver \
  libva-nvidia-driver.i686 \
  libva-nvidia-driver.x86_64

# Codecs for Intel
rpm-ostree install -y intel-media-driver
```

Please note that in **Fedora Atomic** installations, you can setup a custom environment with ``toolbx`` to install others native only applications like a traditional OS. See the oficial ``toolbx`` guide for more details.

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

Steam is the only application that I recommend to install natively:

```bash
# Steam & SteamVR
# SteamVR works only with native application
rpm-ostree install -y steam
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

## In Game Utilities

Proton GE compatibility layer for non Steam games and applications:

```bash
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

Unfortunately, VR on Linux is very experimental yet and is even more harder on immutable OS. Please remember that only the Steam native application can run SteamVR titles on Linux, so we will not recommend any application for VR on Fedora Atomic.

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

Sunshine will works best with native application, so you must manually download the latest .RPM version from website at <https://github.com/LizardByte/Sunshine/releases>. Once downloaded, use the command below to install it:

```bash
rpm-ostree install -y ./sunshine*.rpm
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

Linux is always improving on gaming, but please be aware that most online games does not work due to anti-cheat programs.

Have a good gaming!
