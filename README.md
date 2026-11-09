# SillyTavern QoL Pack

English · [Русский](README.ru.md)

Small quality-of-life improvements for SillyTavern. The first module shows the remaining budget of your saved OpenRouter key.

[**Download the latest release**](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest)

## Install

1. Download **SillyTavern-QoL-Pack-&lt;version&gt;.zip** and extract it anywhere, such as Downloads.
2. Open `Install-Windows.cmd`, `Install-macOS.command`, or run `Install-Linux.sh` in a terminal.
3. Choose your SillyTavern folder and confirm installation.
4. Restart SillyTavern and reload the browser page.

Run the installer on the computer hosting SillyTavern. Requires Node.js 20.12+ and SillyTavern 1.19+.

Select OpenRouter and an active saved key. A key icon appears beside **API Connections**. It opens a compact budget widget. The interface follows SillyTavern’s language: Russian or English as the fallback.

<img width="614" height="468" alt="CleanShot 2026-11-09 at 02 47 17@2x" src="https://github.com/user-attachments/assets/30e6dcca-eb1e-4b27-ad20-10558d42ae20" />

## Updates

The widget checks GitHub Releases automatically, with a six-hour cache. An indicator on the key means an update is available.

Open **About & updates → Install v…**, then restart SillyTavern and reload the page. Both the UI and server plugin update together. The same section offers a rollback to the previous installation. Installation and rollback require a SillyTavern administrator.

Versions 0.4.1 and 0.4.2 can update to 0.4.3 directly from the widget. The compatibility download for 0.4.0 is retained only in the transition release 0.4.2. If you are still on 0.4.0 and missed that transition, run the latest installer once.

## Repository

This public repository hosts installable releases and user documentation. The development repository is currently private. Release archives contain the runtime JavaScript, bundled dependencies, license and third-party notices.

Live installation is verified on macOS with SillyTavern 1.19. Windows and Linux launchers have not yet been tested on those systems.
