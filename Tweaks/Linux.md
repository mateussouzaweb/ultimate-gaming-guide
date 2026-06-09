# Linux Gaming Tweaks

## Game Mode for Better Performance

GameMode is a tool for Linux that temporarily optimizes your system's hardware and operating system settings to deliver maximum performance while you play a game.
It runs seamlessly in the background—automatically boosting CPU and GPU speeds, prioritizing your game over desktop apps, and eliminating micro-stutters. 
Once you quit playing, your system instantly reverts to its normal, power-saving state.

**Enable GameMode for Steam (Flatpak Only)**

If you are using the Flatpak version of Steam, you need to grant it permission to talk to the system's GameMode daemon. Run this command once in your terminal:

```bash
# Grant flatpak permission
flatpak override --user --talk-name=org.freedesktop.GameMode com.valvesoftware.Steam
```

**Activate GameMode inside Steam Games**

Now, to apply these performance tweaks to a game, right-click the game in Steam, go to Properties > General, and add this to the Launch Options field:

```bash
gamemoderun %command%
```

**Using GameMode outside Steam**

You can also use GameMode for standalone games, emulators, or others launchers. \
Simply prefix the game executable or launch shortcut command in the terminal like this:

```bash
# Replace <command> with your game executable or launcher
gamemoderun <command>
```

That is it! Your system will now dynamically optimize itself every time the game boots.


## Use of Proton Versions

Proton is a compatibility layer developed by Valve that allows Windows games to run seamlessly on Linux operating systems. Because games use different graphic engines and technologies, choosing the right version of Proton can drastically improve performance and compatibility.

- **Proton Experimental**: The staging ground for upcoming stable Proton releases. It features bleeding-edge updates, new feature implementations, and continuous performance optimizations.

- **Proton Stable**: Major numbered releases (e.g., Proton 9.0, Proton 10.0). These are thoroughly tested, highly reliable builds meant to offer a baseline "plug-and-play" experience for the vast majority of verified games.

- **Proton Hotfix**: An emergency build deployed by Valve to immediately address broken games, intrusive launcher updates, or day-one release crashes. Only use this if a game completely refuses to boot or a recent update breaks playability. It lacks broad performance improvements.

- **Community Versions**: Independent forks maintained by the Linux community (such as GE-Proton). These versions include custom patches, bleeding-edge media foundation fixes for broken game videos, and specific game tweaks not found in official builds.

Choosing the right version of Proton ensures maximum performance and compatibility while keeping your game library trouble-free.

**How to change Proton versions in Steam?**

To force a specific game to use a different version of Proton, right-click the game in Steam, go to **Properties** > **Compatibility**, check "**Force the use of a specific Steam Play compatibility tool**," and select your desired version from the dropdown menu.

**What is the best proton version to use?**

*Always try Proton Experimental first*. It contains the latest engine overhauls and synchronization fixes needed to close the performance gap between Linux and Windows.

Summary of best choices:

- **For 95% of games**: Stick with **Proton Experimental**. It gives you the closest performance parity to Windows by utilizing modern Linux kernel sync features (like NTSYNC).

- **For older or retro titles**: If Experimental introduces a new bug, **Proton Stable** is your safest bet for older Direct3D 9/11 titles that do not require cutting-edge translation features.

- **For games with unplayable cutscenes**: If a game boots but videos show up as a blank screen or color bars, immediately jump to a **Community Version** (GE-Proton) to utilize its custom media codecs.

- **For day-one game updates**: Only switch to **Proton Hotfix** if an unexpected game update or brand-new release completely prevents the game from launching.