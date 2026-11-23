# SillyTavern QoL Pack

English · [Русский](README.ru.md)

Small quality-of-life improvements for SillyTavern.

[**Download the latest release**](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/releases/latest)

## Features

- **OpenRouter key budget:** See your saved key’s remaining budget, reset time and what you spent today, and get a notice when the limit changes or runs low. Open the widget using the key beside **API Connections**.
- **Model and reply cost:** Identify the model family beside each OpenRouter reply. Tap the icons to reveal the model’s full name, what the reply cost, which provider served it and what caching saved.
- **Quick model picker:** Switch the OpenRouter model in two taps from the button beside Send: your starred models first, then the recent ones, then a search over every model. See [Quick model picker](#quick-model-picker).
- **Swipe with another model:** When you swipe or regenerate the last reply, tap another model to write it instead, or to write one more swipe with it; your selected model stays as it is. See [Swipe with another model](#swipe-with-another-model).
- **Continue and prefill on Claude 4.6+ and Gemini 3.6+:** Continue, impersonate, extensions’ background requests, **Start Reply With** and prefill presets work on Claude 4.6 and later and on Gemini 3.6 and later through OpenRouter, which otherwise refuses them. On by default; see [Continue and prefill on Claude 4.6+ and Gemini 3.6+](#continue-and-prefill-on-claude-46-and-gemini-36).
- **Reasoning Effort “Minimum” on models that must reason:** With **Reasoning Effort** on **Minimum** and **Request model reasoning** off, a model that cannot stop reasoning through OpenRouter (GPT-5, Gemini, GLM 5.3 and others) answers with the least reasoning it allows instead of failing with “Reasoning is mandatory for this endpoint and cannot be disabled”; every other request goes out exactly as SillyTavern built it.
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

Your **Model Providers** selection, including its priority order, and **Allow fallback providers** choice in **API Connections** are remembered separately for each OpenRouter model. Switch through either list, `/model` or a connection profile, and that model’s choices return. A model you have not configured leaves the provider choice to OpenRouter; clearing the selection is remembered too. Your current selection is kept when the feature first loads. A connection-bound preset restores its saved provider choices, including an empty list, and replaces the remembered choice for its model. Most saved presets contain these choices even if you never changed them. A connection profile that loads such a preset restores that snapshot; without it, profiles share the model’s latest choice.

## Swipe with another model

With OpenRouter under Chat Completion, a swipe or a Regenerate of the last reply shows a strip at the top of the new reply, with your starred models and then the recent ones. While the reply is written it reads “Sonnet 5.5 is writing… **Instead:** …”: tap a model to stop it and write the same swipe with that model. Once it has finished, **Again with:** makes one more swipe with the model you tap and keeps the finished one. Models that don’t fit on one line are under “+N”. The strip goes away as soon as you leave that swipe or send a message, and a new reply doesn’t get one.

Your selected model, the dropdown in **API Connections** and your settings don’t change: only that one swipe is written by the other model. Its model badge, reply cost and spending name that model, and it joins your recent models. Continue on such a swipe goes to the model that wrote it, unless you have selected another model since. If the other model has a smaller context, that swipe gets only as much context as the model allows. With **Prompt caching**, a swipe with another model only reads what that model already saved in the chat; once the model has written in the chat within the hour, it also writes, so the next swipe with it reads.

A swipe with another model and its Continue use that model’s remembered providers for the request. Your selected model’s provider controls stay as they are.

To hide the strip, clear **Swipe with another model while swiping** in **Extensions → SillyTavern QoL Pack → Settings**.

## Continue and prefill on Claude 4.6+ and Gemini 3.6+

Through OpenRouter, Claude 4.6 and later models refuse a request that ends on the reply itself; Opus 4.6, Sonnet 4.6 and Opus 4.7 also refuse one that ends on the reply followed by a system message. Gemini 3.6 and later and Gemini 3.5 Flash Lite refuse both. SillyTavern sends such a request for Continue with **Continue prefill** ticked, for every reply while **Start Reply With** holds text, with a preset whose last prompt is an assistant prompt, for a send with an empty input box after a reply, and on those three Claude models and on Gemini for Continue, impersonate and an extension’s background request (a summary, for example) under Prompt Post-Processing None or Merge. Without the pack each of them fails with “Provider returned error” (a background request with “Bad Request”), and a failed regenerate also takes the reply off the screen.

The pack sends such a request in a form the model accepts. It adds SillyTavern’s Continue instruction after the reply as your message, and on the three Claude models and on Gemini it sends the system messages after the last reply as your messages. A Continue then goes on from where the reply stopped, as it does with **Continue prefill** cleared. A prefill no longer steers the reply: the model starts the reply itself, and SillyTavern still puts the prefill text in front of it. Prompt caching reads such a request as it reads any other Continue. Every other request, and every request to other models, goes out exactly as SillyTavern built it. That includes Gemini 3.5 Flash, 3.1 and 2.5, which accept a prefill and continue it (Gemini 2.5 Pro and 2.5 Flash until 1 December 2026, below).

An OpenRouter alias such as `~anthropic/claude-sonnet-latest` counts as the model OpenRouter’s model list says it points to (Sonnet 5.5 for that one), so its requests are fixed as that model’s are. On `~anthropic/claude-haiku-latest` and the Gemini `-latest` aliases OpenRouter used to accept such a request by quietly answering it with an older model that takes a prefill (Haiku 4.5, Gemini 3.5 Flash, Gemini 3.1 Pro Preview); now the request goes to the model the alias points to, at its price, and the prefill no longer steers the reply. An alias that points to any other model goes out unchanged.

From 00:00 UTC on 1 December 2026 the pack also fixes requests to Gemini 2.5 Pro and 2.5 Flash. Google has announced that from that day it answers these two models with newer ones under the same names (Gemini 3.8 Flash and 3.5 Flash Lite), which refuse such requests. From then on, Continue, impersonate and background requests on them keep working instead of failing with “Provider returned error”, as on Gemini 3.6, and a prefill no longer steers the reply. Until then their requests go out unchanged, and the prefill works as before. Google calls the date the earliest possible. If the switch comes later, the pack still changes these requests from 1 December, although the models would have accepted them, and the prefill stops steering the reply a little early. Gemini 2.5 Flash Lite and other 2.5 models are not affected.

It is on by default. To send SillyTavern’s request unchanged, and get the error back, clear **Continue and prefill on Claude 4.6+ and Gemini 3.6+** in **Extensions → SillyTavern QoL Pack → Settings**.

## Prompt caching

Tick **Prompt caching** in **Extensions → SillyTavern QoL Pack → Settings** to use it with Claude and Qwen models through OpenRouter. The pack marks the part of each chat request that repeats the previous request, and the model charges that part at about a tenth of the normal price for an hour after it was last used. Saving it costs more than the normal price once (twice for Claude, 1.25 times for Qwen), so the pack saves only what it expects to be read often enough, and pauses caching in a chat that costs more with it than without it.

The line under the checkbox says whether caching is active, and why not when it is not. Some models cache by themselves, without markers (OpenAI, Gemini, DeepSeek and others): the line says that the model takes no cache markers, and what its own caching saved still shows beside the reply and in the **Saved by caching** row.

### What reduces the saving

Only the start of a prompt that is identical to the previous request’s is read from the cache. A change near the top makes everything after it cost the normal price again. When caching cannot help in the current chat, the pack says so once per session.

- **Dice and random macros before the chat history:** A `{{roll}}` or `{{random}}` in a preset prompt before the chat history changes on every request, so nothing after it repeats. Under Prompt Post-Processing “Semi-strict” the system prompts before the history usually merge into one message with the macro, and then nothing is cached at all. Move the macro to a prompt after the chat history, or switch that prompt off. On Claude Sonnet 4.5 and 4.6, Haiku 4.5 and Opus 4.1, 4.5, 4.6 and 4.7, under Prompt Post-Processing “None”, OpenRouter sends a **System** prompt after the chat history before the history, so there give that prompt the role **User** ([below](#a-preset-prompt-you-switch-on-and-off)). Freaky Frankenstein 5.4 moved its dice to the end, so update an older Freaky Frankenstein 5; in Lucid Loom v3.3, switch off “Chaos Modifier (NSFW)”.
- **Lorebook entries that switch on by keyword near the top:** An entry placed before the character or the chat history comes and goes with its keywords, and each time the history after it costs the normal price. Place such entries at a depth (@D), so they change only the last messages, or make them **Sticky**, so they stay active for a number of messages. On Claude Sonnet 4.5 and 4.6, Haiku 4.5 and Opus 4.1, 4.5, 4.6 and 4.7, under “None”, an entry at a depth with the role System is sent before the chat history too: there, make it **Sticky**.
- **A prompt placed deep in the chat:** A prompt placed in the chat at a depth (an Author's Note, a preset or character prompt in the chat) is put back that many messages from the end on every request, so it and every message after it cost the normal price on every turn. At the usual depth of 4 that is a few messages; at a depth of 30 it can be most of the chat. The status line names the depth when such a prompt keeps more than ten messages, or more than a quarter of the prompt, from the cache. Give it a small depth, or place it before or after the chat history. On Claude Sonnet 4.5 and 4.6, Haiku 4.5 and Opus 4.1, 4.5, 4.6 and 4.7, under “None”, a **System** prompt at a depth is sent before the chat history: one that stays the same costs nothing extra there, and one that comes and goes costs the history each time.
- **Vector Storage for chats:** With **Vector Storage → Enabled for chat messages** on, Vector Storage rebuilds a block of past messages near the top on every request and takes those messages out of the history, so almost nothing repeats. The status line names it. Switch it off where you want caching to save.
- **Frequent summaries:** With **Summarize** placed before or after the main prompt, each new summary changes the prompt near the top once. Summarize less often, for example every 20 messages instead of every 10. Memory Books costs one turn when it creates a memory and hides the summarised messages; its memories are lorebook entries near the top, so a memory that switches on by keyword is the lorebook case above, unless memories are made constant entries.
- **Continue, impersonate and summaries on Qwen under Prompt Post-Processing “None” or “Merge”:** Under these modes SillyTavern sends its instruction for a Continue or an impersonate, and Summarize its request for a summary, as a system message at the end, and Qwen then reads at most the prompts before the chat history from the cache; the history costs the normal price. A reply after a system prompt at the end of the chat appears or changes (a prompt at depth 0, or a group nudge naming another character) reads no more than that either. Under “Semi-strict” the same requests read the whole prompt from the cache, unless dice or random macros sit before the chat history (above). With “Continue prefill” on, a Continue reads the whole prompt under any mode. Claude models are not affected.
- **Gaps of more than an hour:** A saved prompt lasts an hour after it was last used. After a longer gap, the next message pays to save it again.
- **A chat that has outgrown its context size:** Once the chat no longer fits the context size, SillyTavern leaves out its oldest messages, so the history changes at its start on every turn and only the prompts before it are cached. Tick **Cache long chats** ([below](#cache-long-chats)), raise the context size if the model allows it, hide or summarize old messages, or continue in a new chat.

A swipe or a regenerate reads the whole request from the cache. After a change near the top (a prompt switched, an edit), the first swipe saves the request again and the swipes after it read it, as the next message does. An edit, a deleted or hidden message costs one turn at the normal price, then the chat repeats again.

#### A preset prompt you switch on and off

Switching a prompt changes the request from that prompt on: the next request, a swipe or a message, pays to save everything after it once more, and the requests after it read it. Measured on Claude Sonnet 4.5 in a short test chat of about 2,000 tokens, with a prompt at the top of the prompt order: the swipe right after switching it on cost $0.0122, the next swipe $0.0010 and the next message $0.0016, where each would cost about $0.0063 without caching. Where the prompt sits in the Prompt Manager is not always where the model receives it:

- On Claude Sonnet 4.5 and 4.6, Haiku 4.5 and Opus 4.1, 4.5, 4.6 and 4.7, under Prompt Post-Processing “None”, OpenRouter sends every **System** prompt before the chat history, also one placed below **Chat History**. A System prompt you switch therefore costs the whole history once more, wherever it stands. Placed below **Chat History**, or directly above it below the prompts that never change, it leaves those prompts cached.
- A prompt with the role **User**, placed directly below **Chat History**, is sent as the end of your newest message. Switching it leaves the history cached; only the last reply and your newest message are not read. But the model then reads it as something you said, not as a rule of the preset: it may follow it less strictly, or answer it. Try it on your own prompt and keep it only if the replies stay as you want them.
- Under Prompt Post-Processing “Semi-strict” a System prompt below **Chat History** is sent the same way as a User prompt, and every prompt above the history is one block: switching any of those costs everything.
- Switching back within an hour reads what was saved before, up to the message where you switched.

### Caching diagnostics

Open **Caching diagnostics** in the pack’s **Settings**, or **Open diagnostics** in the caching notice. It works on desktop and phones without developer tools. It shows why a request was left unmarked, the reads and writes the pack expected, and the reads, writes and cost OpenRouter reported. Missing usage is unknown, not zero; a notice about little repetition does not itself mean caching lost money.

When you report that caching did not save what it should:

1. Choose **Start session** and close the window.
2. Play as usual for as long as you need: send messages, swipe, switch preset prompts, change the model or **Start Reply With**. The pack records every request and what you changed between requests, and generates nothing itself. A notice confirms the start; while a session runs, the diagnostics button in the pack’s **Settings** says so.
3. Come back to **Caching diagnostics** and choose **Stop session**.
4. Choose **Download JSON** and attach the file to an [issue](https://github.com/AmadeusTwi/sillytavern-qol-pack-releases/issues). If the download does not work on your phone, use **Copy JSON**, or select the JSON at the bottom and copy it.

A running session survives a page reload: after the reload a notice reminds you that it is still recording. Download the file before you reload a page with a stopped session, or it is gone. A long session keeps its newest requests (about 500 in an ordinary chat); the window and the file say how many older ones were dropped.

The file has no prompt text, character, chat, preset or lorebook names: sources and prompts have names local to the file, and texts are sizes and fingerprints. Model, provider and request IDs remain. Where a request stopped repeating the one before, the pack keeps the changed text as an excerpt. Excerpts go into the file only if you open the list of excerpts, read them and tick **Include in the file** for each one you want to share (or **Include all**). Excerpts can contain private text, and a file with excerpts is not anonymous.

While a session runs, it is kept in this browser’s storage, without whole prompts but with the excerpts. **Stop session**, **Clear diagnostics** and SillyTavern’s **Clean extension data** for the pack remove it from the storage. Nothing is uploaded.

A session you forget ends by itself three days after its last request, or after its stop if you stopped it and left the page open. Everything it recorded is removed, excerpts included, so there is nothing left to download. A notice says so the next time you open SillyTavern, or right away if the page is open, and **Caching diagnostics** shows when the last request was until you start a new session. Each request starts the three days again, so a session you play in every day, or on Friday evening and again on Monday morning, keeps running.

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
