# SillyTavern QoL Pack

English · [Русский](README.ru.md)

Small quality-of-life improvements for SillyTavern.

[**Download the latest release**](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest)

## Features

- **OpenRouter key budget:** See your saved key’s remaining budget, reset time and what you spent today, and get a notice when the limit changes or runs low. Open the widget using the key beside **API Connections**.
- **Model and reply cost:** Identify the model family beside each OpenRouter reply. Tap the icons to reveal the model’s full name, what the reply cost, which provider served it and what caching saved.
- **Quick model picker:** Switch the OpenRouter model in two taps from the button beside Send: your starred models first, then the recent ones, then a search over every model. See [Quick model picker](#quick-model-picker).
- **Prompt caching:** Pay about a tenth of the normal price for the part of each prompt that repeats, with Claude and Qwen models through OpenRouter. Off by default; see [Prompt caching](#prompt-caching). The key widget’s Details show what caching saved in a **Saved by caching** row.

Preferences: **Extensions → SillyTavern QoL Pack → Settings**.

## Install

Run the installer on the device hosting SillyTavern. Requires SillyTavern 1.19+ and Node.js 20.12+.

1. Download **SillyTavern-QoL-Pack-&lt;version&gt;.zip** and extract it anywhere, such as Downloads.
2. Run `Install-Windows.cmd`, `Install-macOS.command`, or `Install-Linux.sh` for your system.
3. Choose **English** or **Русский**, select your SillyTavern folder, and confirm.
4. Restart SillyTavern and reload the browser page.

Select OpenRouter and an active saved key to show the budget icon. The interface follows SillyTavern’s language, with English as the fallback.

### Android / Termux

Stop SillyTavern with **Ctrl+C**. Paste these commands into Termux from any folder to install the latest release:

```bash
pkg install curl unzip &&
zip_url="$(curl -fsSL https://api.github.com/repos/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest | grep -o 'https://[^"]*\.zip"' | head -1 | tr -d '"')" &&
curl -fL "$zip_url" -o "$HOME/qol-pack.zip" &&
unzip -o "$HOME/qol-pack.zip" -d "$HOME/qol-pack-installer" &&
node "$HOME/qol-pack-installer/SillyTavern-QoL-Pack/resources/bin/install.mjs"
```

Follow the wizard, entering your SillyTavern path if needed, usually `~/SillyTavern`. Start SillyTavern again and reload the page.

After installation, you can delete `~/qol-pack.zip` and `~/qol-pack-installer`.

## Updates

Open **Extensions → SillyTavern QoL Pack** or **About & updates** in the key widget to install updates or roll back. Restart SillyTavern and reload the page after installation. Installing updates and rolling back require a SillyTavern administrator.

**What’s new** shows only the releases you missed. **Changelog** opens the complete release history.

## Quick model picker

With OpenRouter under Chat Completion, a button with the current model’s logo sits left of Send, with a short name on wider screens. Tap it to open the list: the current model on top, then your **Starred** models, the **Recent** ones (the last five that wrote a reply in your chats) and **All models** by vendor, with each model’s context size and price. Type in the search field to find any model, and tap a row to switch to it. On a phone the list opens as a sheet from the bottom; drag it down or tap outside it to close it.

Tap the star beside a model to keep it under **Starred**. Stars and recent models follow your SillyTavern user to every device. A starred model that OpenRouter no longer lists stays greyed out until you remove its star.

The picker sets the same model as the dropdown in **API Connections**, so connection profiles and presets work as before, and the button always shows the model SillyTavern uses. To hide the button, clear **Quick model picker beside Send** in **Extensions → SillyTavern QoL Pack → Settings**.

When you switch to a model with a smaller context, SillyTavern lowers the context size to that model’s limit and never raises it back. It does the same to the temperature: a switch to a Claude model lowers it to 1.0, and it stays 1.0 on the next model. The pack remembers the context size and the temperature you set and restores them after any model switch, from the picker, the dropdown, `/model` or a connection profile, as far as the current model allows. A value you set by hand, or a preset sets, becomes the one it restores. This is always on and has no setting.

## Prompt caching

Tick **Prompt caching** in **Extensions → SillyTavern QoL Pack → Settings** to use it with Claude and Qwen models through OpenRouter. The pack marks the part of each chat request that repeats the previous request, and the model charges that part at about a tenth of the normal price for an hour after it was last used. Saving it costs more than the normal price once (twice for Claude, 1.25 times for Qwen), so the pack saves only what it expects to be read often enough, and pauses caching in a chat that costs more with it than without it.

The line under the checkbox says whether caching is active, and why not when it is not. Some models cache by themselves, without markers (OpenAI, Gemini, DeepSeek and others): the line says that the model takes no cache markers, and what its own caching saved still shows beside the reply and in the **Saved by caching** row.

### What reduces the saving

Only the start of a prompt that is identical to the previous request’s is read from the cache. A change near the top makes everything after it cost the normal price again. When caching cannot help in the current chat, the pack says so once per session.

- **Dice and random macros before the chat history:** A `{{roll}}` or `{{random}}` in a preset prompt before the chat history changes on every request, so nothing after it repeats. Under Prompt Post-Processing “Semi-strict” the system prompts before the history usually merge into one message with the macro, and then nothing is cached at all. Move the macro to a prompt after the chat history, or switch that prompt off. Freaky Frankenstein 5.4 moved its dice to the end, so update an older Freaky Frankenstein 5; in Lucid Loom v3.3, switch off “Chaos Modifier (NSFW)”.
- **Lorebook entries that switch on by keyword near the top:** An entry placed before the character or the chat history comes and goes with its keywords, and each time the history after it costs the normal price. Place such entries at a depth (@D), so they change only the last messages, or make them **Sticky**, so they stay active for a number of messages.
- **A prompt placed deep in the chat:** A prompt placed in the chat at a depth (an Author's Note, a preset or character prompt in the chat) is put back that many messages from the end on every request, so it and every message after it cost the normal price on every turn. At the usual depth of 4 that is a few messages; at a depth of 30 it can be most of the chat. The status line names the depth when such a prompt keeps more than ten messages, or more than a quarter of the prompt, from the cache. Give it a small depth, or place it before or after the chat history.
- **Vector Storage for chats:** With **Vector Storage → Enabled for chat messages** on, Vector Storage rebuilds a block of past messages near the top on every request and takes those messages out of the history, so almost nothing repeats. The status line names it. Switch it off where you want caching to save.
- **Frequent summaries:** With **Summarize** placed before or after the main prompt, each new summary changes the prompt near the top once. Summarize less often, for example every 20 messages instead of every 10. Memory Books costs one turn when it creates a memory and hides the summarised messages; its memories are lorebook entries near the top, so a memory that switches on by keyword is the lorebook case above, unless memories are made constant entries.
- **Continue and impersonate on Qwen under Prompt Post-Processing “None”:** Under “None” SillyTavern sends its instruction for a Continue or an impersonate as a system message at the end, and Qwen then reads only the prompts before the chat history from the cache; the history costs the normal price. Under “Semi-strict” the same requests read the whole prompt from the cache, unless dice or random macros sit before the chat history (above). Claude models are not affected.
- **Gaps of more than an hour:** A saved prompt lasts an hour after it was last used. After a longer gap, the next message pays to save it again.
- **A chat that has outgrown its context size:** Once the chat no longer fits the context size, SillyTavern leaves out its oldest messages, so the history changes at its start on every turn and only the prompts before it are cached. Tick **Cache long chats** ([below](#cache-long-chats)), raise the context size if the model allows it, hide or summarize old messages, or continue in a new chat.

A swipe or a regenerate reads the whole request from the cache. An edit, a deleted or hidden message costs one turn at the normal price, then the chat repeats again.

### Cache long chats

Tick **Cache long chats** under **Prompt caching** for chats that no longer fit their context size. SillyTavern leaves out the oldest messages of such a chat one or two at a time, so the history starts at a different message on every turn and only the prompts before it are read from the cache. With the box ticked, the pack leaves out a larger chunk of the oldest messages at once, and the following turns start the history at the same message until the next chunk is due, so the whole history between two chunks is read from the cache. In a chat that is already too long, the first chunk is left out on the next request. It is off by default.

The model reads less of the oldest history in exchange. Right after a chunk it reads about 70% of the history SillyTavern would send, never less than half; turn by turn that grows back to all of it before the next chunk, about 85% on average (simulated at context sizes of 32k and more). At a 50k context such a chat costs about a fifth of what it costs without caching, where prompt caching alone saves little (simulated). Measured in a real chat at a 32k context on Claude Haiku 5.5: a full cycle cost about 12% of what the same turns cost without caching, and the model read 70% of the history right after a chunk and 84% on average.

Leave it off when old details matter more than the price, or when the chat is cheap anyway, at a small context size or on a cheap model. The same list opens under the checkbox as **When to leave it off**.

With **Summarize**, set its **Prompt builder** to **Raw, blocking** or **Raw, non-blocking**: they summarize the chat itself, so every message is summarized whatever the pack leaves out. **Classic, blocking** summarizes the prompt as it is sent, so a message left out in a chunk before the next summary is never summarized. With it, keep **Update every** at about half the messages that fit the context or fewer, and do not use the automatic interval, which counts all of them.

Nothing in the chat is hidden, deleted or changed: the messages left out are only not sent, as SillyTavern already does with messages that do not fit. The dashed line in the chat marks the first message the model reads. Untick the box, and the next request is again the one SillyTavern builds.

With it on, a larger context size is affordable: a long chat at a 32k context costs about what the same chat costs at 8k without caching, and the model reads about five times as much of its history (simulated). A very small context size saves less: such a chat is cheap already, and a chunk has to take up to half of the history to last ten replies.

With **Example Messages Behavior** on **Gradual push-out** (SillyTavern's default), the character's example dialogue is left out once the chat no longer fits: otherwise it slips in and out of the prompt and costs the cached history. **Always include examples** and **Never include examples** are kept as set.

It leaves out nothing where it cannot save, and SillyTavern trims the chat as usual: while prompt caching is not active, with Vector Storage for chats on, where the prompt changes before the chat history from turn to turn (dice or a random macro there, a group chat with the default preset), and while the chat still fits. The line under the checkbox says whether it is active in this chat, and why not when it is not.

The chunk size is chosen for you: 30% of the history, more at a small context size so that a chunk lasts ten replies, and never more than half. To set it yourself, enter a share from 10 to 50 in **Long chats: chunk size, % of history** under **Advanced** in the Settings. A larger chunk saves more and leaves the model less history; a smaller one the reverse. Leave the field empty for the automatic size.

## Removing the pack

1. Open **Extensions → Manage extensions**, click the trash can on the **SillyTavern QoL Pack** row and tick **Also clean up extension data**.
2. Delete the `plugins/openrouter-key-budget` folder inside your SillyTavern folder.
3. Restart SillyTavern.

## Troubleshooting

### “Install extension” fails

Use the ZIP installer for this pack. **Install extension** clones browser extensions from Git repositories and cannot install the server component.

A release-page URL produces `not valid: is this a git repository?`. Follow the installation steps above instead.

### Updating from v0.4.0

Run the latest installer once, then use the widget for future updates.

## Repository

This repository hosts downloads and user documentation. The source repository is currently private.
