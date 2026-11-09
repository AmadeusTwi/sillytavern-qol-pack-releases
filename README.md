# SillyTavern QoL Pack

English · [Русский](README.ru.md)

Small quality-of-life improvements for SillyTavern.

[**Download the latest release**](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest)

## Features

- **OpenRouter key budget:** See your saved key’s remaining budget and reset time. Open the widget using the key beside **API Connections**.
- **Model badges:** Identify the model family beside each OpenRouter reply. Tap the icons to reveal the model’s full name.

## Install

Run the installer on the device hosting SillyTavern. Requires SillyTavern 1.19+ and Node.js 20.12+.

1. Download **SillyTavern-QoL-Pack-&lt;version&gt;.zip** and extract it anywhere, such as Downloads.
2. Run `Install-Windows.cmd`, `Install-macOS.command`, or `Install-Linux.sh` for your system.
3. Choose **English** or **Русский**, select your SillyTavern folder, and confirm.
4. Restart SillyTavern and reload the browser page.

Select OpenRouter and an active saved key to show the budget icon. The interface follows SillyTavern’s language, with English as the fallback.

### Android / Termux

Stop SillyTavern with **Ctrl+C**. Paste these commands into Termux from any folder to install **v0.5.2**:

```bash
pkg install curl unzip &&
curl -fL "https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/download/v0.5.2/SillyTavern-QoL-Pack-0.5.2.zip" -o "$HOME/qol-pack.zip" &&
unzip -o "$HOME/qol-pack.zip" -d "$HOME/qol-pack-installer" &&
node "$HOME/qol-pack-installer/SillyTavern-QoL-Pack/resources/bin/install.mjs"
```

Follow the wizard, entering your SillyTavern path if needed, usually `~/SillyTavern`. Start SillyTavern again and reload the page.

After installation, you can delete `~/qol-pack.zip` and `~/qol-pack-installer`.

## Updates

Open **Extensions → SillyTavern QoL Pack** or **About & updates** in the key widget to install updates or roll back. Restart SillyTavern and reload the page after installation. Installing updates and rolling back require a SillyTavern administrator.

**What’s new** shows only the releases you missed. **Changelog** opens the complete release history.

## Troubleshooting

### “Install extension” fails

Use the ZIP installer for this pack. **Install extension** clones browser extensions from Git repositories and cannot install the server component.

A release-page URL produces `not valid: is this a git repository?`. Follow the installation steps above instead.

### Updating from v0.4.0

Run the latest installer once, then use the widget for future updates.

## Repository

This repository hosts downloads and user documentation. The source repository is currently private.
