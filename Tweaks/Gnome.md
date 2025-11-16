# Gnome Tweaks

## Design Tweaks

These commands will automatically optimize the Gnome system with a better UI design and settings:

```bash
# Better Alt+Tab
gsettings set org.gnome.shell.window-switcher current-workspace-only false

# Enable additional window buttons
gsettings set org.gnome.desktop.wm.preferences button-layout "appmenu:minimize,maximize,close"

# Set custom icon theme
wget -qO- https://git.io/papirus-icon-theme-install | env DESTDIR="$HOME/.icons" sh
gsettings set org.gnome.desktop.interface icon-theme "Papirus"
```

## Automatic Login

To activate automatic login on Gnome, you just need to follow these instructions:

```bash
# In the open file, please uncomment these lines and set values as below: 
# -- [daemon]
# -- AutomaticLoginEnable=True
# -- AutomaticLogin=$USER
sudo vim /etc/gdm/custom.conf
```

Since you are disabling login password requirement, it also good to avoid the screen lock with the necessity to type the password:

```bash
gsettings set org.gnome.desktop.lockdown disable-lock-screen true
```

If you want to completely remove the user password:

```bash
sudo passwd --delete $USER
```

Restart the system and see that the automatic login feature is working.