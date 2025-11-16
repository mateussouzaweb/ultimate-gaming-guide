# KDE Tweaks

## Design Tweaks

These commands will automatically optimize the KDE system with a better UI design and settings:

```bash
# Set screen resolution
# 4K / 144hz / 150% scaling
kscreen-doctor output.DP-3.mode.3840x2160@144
kscreen-doctor output.DP-3.scale.1.5 

# Set dark theme
kwriteconfig6 --notify --file kdeglobals --group KDE \
  --key LookAndFeelPackage "org.kde.breezedark.desktop"

# Set custom icon theme
wget -qO- https://git.io/papirus-icon-theme-install | env DESTDIR="$HOME/.local/share/icons" sh
kwriteconfig6 --notify --file kdeglobals --group Icons --key Theme "Papirus-Dark"
```

Manual tweaks for better gaming centric design:

- Configure menu launcher to show applications as Grid.
- Configure menu launcher to show applications sorted from to A-Z.
- Remove any Wine menu from launcher.
- Hide all applets and leave only the clock visible.

## Automatic Login

To activate automatic login on KDE Plasma, you just need to follow these instructions:

```bash
# In the open file, please uncomment these lines and set values as below: 
# -- [Autologin]
# -- Relogin=true
# -- Session=plasma
# -- User=$USER
sudo vim /etc/sddm.conf
```

If you want to completely remove the user password:

```bash
sudo passwd --delete $USER
```

Since you are disabling login password requirement, it also good to avoid the screen lock with the necessity to type the password:

- Open "System Settings".
- Go to "Security & Privacy" > "Screen Locking".
- Set "Lock Screen automatically" as "Never".
- Uncheck the option "Lock after waking from sleep".
- Apply changes.

To avoid typing the password on open the system secrets manager, remove KWallet password:

- Open "KWalletManager".
- In the GUI, use the option "Change Password".
- A prompt for a new password will be open.
- Leave empty and click "OK".
- Confirm the change.
- Close the application.

Restart the system and see that the automatic login feature is working.