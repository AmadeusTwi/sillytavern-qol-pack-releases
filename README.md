# SillyTavern QoL Pack

English · [Русский](README.ru.md)

Small quality-of-life improvements for SillyTavern: a saved-key budget widget and model identification beside OpenRouter replies.

[**Download the latest release**](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest)

## Install

1. Download **SillyTavern-QoL-Pack-&lt;version&gt;.zip** and extract it anywhere, such as Downloads.
2. Open `Install-Windows.cmd`, `Install-macOS.command`, or run `Install-Linux.sh` in a terminal.
3. Choose your language, then your SillyTavern folder and confirm installation.
4. Restart SillyTavern and reload the browser page.

Run the installer on the computer or phone hosting SillyTavern. Requires Node.js 20.12+ and SillyTavern 1.19+. For Android, follow the Termux steps below.

On every platform, the wizard starts with **Language / Язык**: English or Русский. It preselects the system locale, with English as the fallback. This only affects the installer. To skip the question, run `node resources/bin/install.mjs --lang en` or `--lang ru` from the extracted folder.

Select OpenRouter and an active saved key. A key icon appears beside **API Connections**. It opens a compact budget widget. The interface follows SillyTavern’s language: Russian or English as the fallback.

<img width="614" height="468" alt="CleanShot 2026-11-09 at 02 47 17@2x" src="https://github.com/user-attachments/assets/30e6dcca-eb1e-4b27-ad20-10558d42ae20" />

### Android / Termux

If SillyTavern runs on your phone in Termux, stop it with **Ctrl+C**, then paste the following into Termux from any folder. These commands download and install **v0.5.1**:

```bash
pkg install curl unzip &&
curl -fL "https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/download/v0.5.1/SillyTavern-QoL-Pack-0.5.1.zip" -o "$HOME/qol-pack.zip" &&
unzip -o "$HOME/qol-pack.zip" -d "$HOME/qol-pack-installer" &&
node "$HOME/qol-pack-installer/SillyTavern-QoL-Pack/resources/bin/install.mjs"
```

Choose your SillyTavern installation in the wizard and confirm. If it is not found, enter the folder you normally start SillyTavern from, usually `~/SillyTavern`. The installer sets up both components and enables server plugins automatically; your saved OpenRouter key stays in place.

Start SillyTavern as usual and reload its browser page. After installation, use **About & updates** in the widget for newer versions. You can delete `~/qol-pack.zip` and `~/qol-pack-installer` once installation succeeds.

## Model identification

OpenRouter replies show the OpenRouter icon alongside the model family’s native SillyTavern logo when available: Claude, OpenAI, DeepSeek, Z.AI, Google and others.

Tap or click the icon group to reveal the readable model name from the **API Connections** model list. Tap again, click elsewhere or press Escape to close it. Enter and Space also work. Long names wrap on narrow screens instead of being clipped.

Each reply and selected swipe uses its own recorded model metadata. Changing your current provider or model does not relabel old replies. If the model is missing from the loaded catalog, a readable form of its saved identifier is used. If no model was recorded, the label says so.

The module respects **User Settings → Model Icons** and document mode. It does not change chat data or make additional OpenRouter requests.

## Updates

The widget checks GitHub Releases automatically, with a six-hour cache. An indicator on the key means an update is available.

Open **About & updates → Install v…**, then restart SillyTavern and reload the page. Both the UI and server plugin update together. The same section offers a rollback to the previous installation. Installation and rollback require a SillyTavern administrator.

Versions 0.4.1 and 0.4.2 can update to 0.4.3 directly from the widget. The compatibility download for 0.4.0 is retained only in the transition release 0.4.2. If you are still on 0.4.0 and missed that transition, run the latest installer once.

## Troubleshooting

### Why does “Install extension” fail?

SillyTavern’s **Install extension** dialog clones a Git repository containing a browser extension. This pack also needs a server plugin, so use the ZIP installer described above to install both components together.

A link ending in `/releases/tag/v…` opens a release page, which Git cannot clone. Pasting it into that dialog produces `not valid: is this a git repository?`. The repository’s main URL also will not install the pack: this repository hosts documentation and release downloads.

## Repository

This public repository hosts installable releases and user documentation. The development repository is currently private. Release archives contain the runtime JavaScript, bundled dependencies, license and third-party notices.
