# Windows Tweaks

## Performance Tweaks

- Make sure to install the latest chipset and GPU driver in the system.
- Set [Power Plan to High Performance](https://help.ableton.com/hc/en-us/articles/115000211304-Using-the-High-performance-power-plan-Windows-) in Control Panel.
- Disable [Fast Startup](https://pureinfotech.com/disable-fast-startup-windows-11-10/) in the Power Options.
- Disable [Xbox Game Bar](https://apps.microsoft.com/store/detail/9NZKPSTSNW4P?hl=pt-br&gl=BR) in Windows Settings.
- Disable [Game Mode](https://support.xbox.com/en-US/help/games-apps/game-setup-and-play/use-game-mode-gaming-on-pc) in Windows Settings (yes, disable).
- Enable [Variable Refresh Rate](https://www.elevenforum.com/t/enable-or-disable-variable-refresh-rate-for-games-in-windows-11.12052/) (VRR) in Graphics Settings.
- Enable [Optimizations for Windowed Games](https://support.microsoft.com/en-us/windows/optimizations-for-windowed-games-in-windows-11-3f006843-2c7e-4ed0-9a5e-f9389e535952) in Graphics Settings.
- On AMD GPUs, enable [Smart Access Memory](https://www.amd.com/en/technologies/smart-access-memory) on BIOS and AMD Software.

## Design Tweaks

- Open "Settings" application.
- Go to "Personalization" > "Colors" and set color mode as "Dark".
- Go to "Personalization" > "Start" and tweak the settings based on you preferences.
- Go to "Personalization" > "Taskbar" and tweak the settings based on you preferences.
- Go to "System" > "Multitasking" > and change the Alt+Tab experience to not show/include Microsoft Edge tabs.

## Automatic Login

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