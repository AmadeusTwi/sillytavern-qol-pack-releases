# SillyTavern QoL Pack

Small quality-of-life improvements for SillyTavern. The first module shows the remaining budget of your saved OpenRouter key.

[**Download the latest release**](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest)

## Install

1. Download the ZIP and extract it anywhere, such as Downloads.
2. Open `Install-Windows.cmd`, `Install-macOS.command`, or run `Install-Linux.sh` in a terminal.
3. Choose your SillyTavern folder and confirm installation.
4. Restart SillyTavern and reload the browser page.

Run the installer on the computer hosting SillyTavern. Requires Node.js 20.12+ and SillyTavern 1.19+.

Select OpenRouter and an active saved key. A key icon appears beside **API Connections**. It opens a compact budget widget. The interface follows SillyTavern’s language: Russian or English as the fallback.

## Updates

The widget checks GitHub Releases automatically, with a six-hour cache. An indicator on the key means an update is available.

Open **About & updates → Install v…**, then restart SillyTavern and reload the page. Both the UI and server plugin update together. The same section offers a rollback to the previous installation. Installation and rollback require a SillyTavern administrator.

## По-русски

1. Скачайте ZIP из последнего релиза и распакуйте в любую папку.
2. Откройте установщик для своей системы: `Install-Windows.cmd`, `Install-macOS.command` или `Install-Linux.sh`.
3. Выберите папку установленной SillyTavern и подтвердите установку.
4. Перезапустите SillyTavern и обновите страницу.

При выбранном OpenRouter и сохранённом активном ключе рядом с API Connections появится ключик. Обновления пакета устанавливаются из раздела **«О пакете и обновлениях»** внутри виджета. После них тоже нужен перезапуск SillyTavern.

## Repository

This public repository hosts installable releases and user documentation. The development repository is currently private. Release archives contain the runtime JavaScript, bundled dependencies, license and third-party notices.

Live installation is verified on macOS with SillyTavern 1.19. Windows and Linux launchers have not yet been tested on those systems.
