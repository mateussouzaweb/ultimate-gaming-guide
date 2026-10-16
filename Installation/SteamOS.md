# Gaming on SteamOS

Steam is great and you already have almost everything built into it for gaming. This guide will only cover a few additional steps:

- If not already installed, install Steam OS natively.
- Once you get into Gaming mode, perform Steam setup and switch to the Desktop mode.
- Open the ``Konsole`` application and run the commands below to perform automated extra gaming setup.
- Steam already is installed and is the only application that I recommend to use natively.

## System Update

Perform a full system update to make sure everything is updated:

```bash
# Update system packages and reboot
steamos-update check
steamos-update
systemctl reboot
```

## Gaming Applications

Now that the system is installed, you can install extra gaming platforms and additional applications. NiceDeck will be used to help with the installation of gaming applications and emulators because it offers additional automation for applications that usually are manually downloaded.

Here is the instructions for usage with Steam OS:

```bash
# Download executable
REPOSITORY="https://github.com/mateussouzaweb/nicedeck"
sudo wget $REPOSITORY/releases/latest/download/nicedeck-linux-amd64 -O ./nicedeck
sudo chmod +x ./nicedeck

# Self installer
./nicedeck install-programs --programs=nicedeck

# Gaming Stores & Launchers
# Note that Steam is not included in the list
./nicedeck install-programs --programs=epic-games
./nicedeck install-programs --programs=ea-app
./nicedeck install-programs --programs=ubisoft-connect
./nicedeck install-programs --programs=gog-galaxy
./nicedeck install-programs --programs=amazon-games
./nicedeck install-programs --programs=battle-net
./nicedeck install-programs --programs=rockstar-games-launcher
./nicedeck install-programs --programs=heroic-games
./nicedeck install-programs --programs=es-de

# Others
./nicedeck install-programs --programs=discord
./nicedeck install-programs --programs=proton-plus

# Streaming
./nicedeck install-programs --programs=moonlight
./nicedeck install-programs --programs=chiaki-ng
./nicedeck install-programs --programs=geforce-now
./nicedeck install-programs --programs=xbox-cloud-gaming

# Browsers
./nicedeck install-programs --programs=brave-browser
./nicedeck install-programs --programs=google-chrome
./nicedeck install-programs --programs=microsoft-edge
./nicedeck install-programs --programs=firefox

# Emulators
./nicedeck install-programs --programs=cemu
./nicedeck install-programs --programs=eden
./nicedeck install-programs --programs=pcsx2
./nicedeck install-programs --programs=rpcs3
./nicedeck install-programs --programs=ryujinx
./nicedeck install-programs --programs=shadps4
./nicedeck install-programs --programs=xenia

./nicedeck install-programs --programs=azahar
./nicedeck install-programs --programs=dolphin
./nicedeck install-programs --programs=duckstation
./nicedeck install-programs --programs=flycast
./nicedeck install-programs --programs=melonds
./nicedeck install-programs --programs=mgba
./nicedeck install-programs --programs=ppsspp
./nicedeck install-programs --programs=redream
./nicedeck install-programs --programs=gopher64
./nicedeck install-programs --programs=vita3k
./nicedeck install-programs --programs=xemu

# Remove temporary copy after installation 
rm ./nicedeck
```

Additional applications for specific use cases are available in the next topics.

## Virtual Reality

NOTE: Only the Steam native application can run SteamVR titles on Linux.

```bash
# ALVR - See install instructions at https://github.com/alvr-org/ALVR
```

## Racing Steering Wheel

Oversteer is compatible with many hardware vendors:

```bash
# Flatpak version 
flatpak install -y flathub io.github.berarma.Oversteer

# Flatpak permissions
DESTINATION="/etc/udev/rules.d/"
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

Sunshine is a solid application for streaming and remote gaming:

```bash
# Sunshine
flatpak install -y flathub dev.lizardbyte.app.Sunshine
flatpak run --command=additional-install.sh dev.lizardbyte.app.Sunshine
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
