# Hina — user guide

Hina is a VTuber companion that lives on your screen: an animated avatar that talks by voice or
text, remembers what you tell her, can act on your computer when you allow it and, if you want,
takes care of your smart home. This guide is for people who installed Hina from the installer. Running from
source belongs to the development repository, not to this guide.

Guide version: 2026-10-09 (Hina 0.3.x, pre-release). The installers are **not code-signed yet**;
your system will warn you, and the steps below explain what to do.

- [1. Install](#1-install)
- [2. API keys](#2-api-keys)
- [3. First conversation](#3-first-conversation)
- [4. Agent (actions on your computer)](#4-agent-actions-on-your-computer)
- [5. Hermes (optional, experimental)](#5-hermes-optional-experimental)
- [6. Update](#6-update)
- [7. Uninstall](#7-uninstall)
- [8. Where your data lives](#8-where-your-data-lives)
- [9. Common problems](#9-common-problems)
- [10. Privacy, license and contact](#10-privacy-license-and-contact)

## 1. Install

Download the file for your system from the
[Releases](https://github.com/Project-H-I-N-A/hina-releases/releases) page. Installers are 200 to
280 MB; the installed app takes about 560 MB. Internet is required: Hina talks to cloud AI services
(see [API keys](#2-api-keys)).

**Windows 10/11** — `Hina Setup x.y.z.exe`. Run it and pick a folder (default
`%LOCALAPPDATA%\Programs\Hina`). SmartScreen will show "Unknown publisher": click *More info* →
*Run anyway*. This happens because the installer is not signed yet.

**macOS (Apple Silicon)** — `Hina-x.y.z-arm64.dmg`. Drag Hina to *Applications*. On first launch
macOS may say the app "is damaged": the download is fine, the app just has no signature. Open
Terminal and run:

```
xattr -cr /Applications/Hina.app
```

Then open Hina normally. It will ask for **Microphone** (to hear you) and, if you use screen vision,
**Screen Recording**, under System Settings → Privacy & Security.

**Linux** — `Hina-x.y.z.AppImage` (make it executable and run), `hina_x.y.z_amd64.deb`
(`sudo apt install ./hina_x.y.z_amd64.deb`) or `hina-x.y.z.tar.xz`. On Wayland Hina uses its own
host so the pet stays above windows; on GNOME it opens as a regular window.

Hina starts as a **pet**: the avatar floats above other windows, without a frame. The tray icon
gives you *Talk (push-to-talk)*, *Look at the screen*, *Stop speaking*, *Show/hide chat*,
*Click-through*, *Always on top* and *Quit*.

## 2. API keys

Hina has no account or subscription of its own: it uses **your** key from an AI provider, and you
pay the provider directly for what you use. On first boot a three-step assistant explains this,
shows the estimated cost per hour of conversation and links the privacy policy.

1. Create a key at a provider. Any of these is enough to chat and use the agent: **Groq** (fast,
   recommended), **Gemini**, **OpenAI**, **OpenRouter** or **xAI**. Live mode (real-time voice) needs
   a Gemini key.
2. Open the **Dashboard** (icon on the avatar's control island or from the chat) → **Settings →
   Keys**, paste the key and save. *Get key ↗* opens the provider's page.
3. Optional, on the same page: **ElevenLabs** or **Cartesia** (higher-quality voices), **Deepgram**
   (streaming hearing). Without them Hina uses the fallback voices and hearing, which already work.

Keys are stored in your system's vault (Credential Manager on Windows, Keychain on macOS, Secret
Service on Linux), never in plain text. The assistant's estimate (October 2026 list prices) is about
US$ 0.40 per hour of conversation with the defaults (brain 0.07, ElevenLabs voice 0.29, Groq hearing
0.04); the worst case, streaming hearing (Deepgram) left on for the whole hour, is about US$ 0.83.

## 3. First conversation

- **By text:** open the chat (island icon or tray → *Show/hide chat*) and type. Enter sends.
- **By voice:** tap the microphone on the control island for automatic listening, or **hold** it
  to talk and release. Tray → *Talk (push-to-talk)* does the same. Under Settings → Hearing you can
  enable the wake word ("hey Hina") and tune how much silence Hina waits before answering.
- **Interrupt:** talk over her or click *Stop speaking* in the tray.
- **Avatar and voice:** the island icons switch the avatar (Live2D, VRM or PNGTuber) and the voice.
  The persona (way of speaking, mood, memories) is edited in Dashboard → **Persona**.
- **Window mode:** from the chat you can *Open in browser*; Hina becomes a regular page
  (`http://127.0.0.1:8000`) with the same controls and the pet closes. *Back to pet mode* returns.
- **Memory:** she remembers across sessions. Dashboard → **Memory** lets you browse, search and
  delete what was kept.

Tip: Hina answers in Portuguese by default. Settings → General → *Interface language* switches the
interface to English; the persona follows the language you speak to her.

## 4. Agent (actions on your computer)

With the agent on, Hina reads files, searches the web, runs commands, opens programs, creates
background tasks and, if you allow it, drives the browser and controls the screen. All of it is
**off until you turn it on**.

1. Dashboard → **Agent** → enable the agent.
2. Choose the **root folder**: the agent only sees that folder (plus the *Authorized extra folders*
   you add). In the pet, *Set Hina's root folder* opens the system picker.
3. Permissions: by default every sensitive action (writing a file, running a command, sending a
   message) **asks for your confirmation** on screen, with the complete arguments. You answer
   *once*, *always* or *deny*. Dashboard → Agent lets you allow or block tool by tool.
4. Reading (files and web) and background tasks (**Kanban**) show up in the pet's activity window;
   each task shows what it did.

What the agent does not do: leave the root folder, use API keys that belong to another service, or
run something you denied. When Hina says she did something, she shows the evidence (command output,
file created).

## 5. Hermes (optional, experimental)

Hermes is an external agent (Nous Research) that can take over Hina's "brain". In this version it
**is not bundled**: you install and configure it on your machine yourself, and Hina uses it through
the `hina-chat` profile. While Hermes is active, the native agent stands by.

Toggle it in Dashboard → **Agent → Hermes**. If Hermes does not answer, Hina warns you and falls
back to the native brain on her own. Treat it as experimental: the Hermes test suite is still being
closed for 1.0.

## 6. Update

Hina checks for new versions at startup and tells you when there is one. Dashboard → **Settings →
Updates** lets you receive **beta versions** (earlier, may have defects) or stable only.

- **Windows and Linux:** the update downloads and installs itself once you accept.
- **macOS:** while the app is unsigned, automatic updates do not work. Download the new `.dmg`,
  replace Hina in *Applications* and run `xattr -cr` again. Your data and keys stay.

On Windows the installer keeps a copy of itself (~216 MB) in `%LOCALAPPDATA%\hina-updater` for
automatic updates; you can delete it by hand without affecting the app.

## 7. Uninstall

**Windows:** Settings → Apps → Hina → Uninstall (or `Uninstall Hina.exe` in the program folder).
Then, to remove everything: `%APPDATA%\Hina` (data, memory, configuration),
`%LOCALAPPDATA%\hina-updater` and the "com.rhayron.hina" entries in Credential Manager.

**macOS:** drag Hina from *Applications* to the Trash. Data in
`~/Library/Application Support/Hina`; keys in Keychain (search "com.rhayron.hina").

**Linux:** delete the AppImage or `sudo apt remove hina`. Data in `~/.config/Hina`; keys in the
system vault (Secret Service).

Deleted data does not come back: Hina's memory lives only in that folder.

## 8. Where your data lives

| What | Where | Leaves your computer? |
|---|---|---|
| Configuration (`config.yaml`), personas, memory, telemetry | data folder above | no |
| API keys | system vault | only to the key's provider |
| Conversations | sent to the AI provider you chose to generate the answer | yes, to the provider |
| Microphone audio | sent to the hearing (STT) provider only while listening is active | yes, to the provider |
| Screen (vision) | only when you trigger *Look at the screen* or enable vision | yes, to the provider |
| Logs | `logs/` in the data folder; the Dashboard's *support bundle* redacts keys | only if you send it |

The full policy is in [PRIVACY.en.md](https://github.com/Project-H-I-N-A/hina-releases/blob/main/PRIVACY.en.md).

## 9. Common problems

- **"Hina could not start" / "The internal server did not respond".** Another Hina is already open
  or something is using port 8000. Close the other instance (tray → Quit) and open again. The log
  path is in the message.
- **"Another service is using Hina's port: identity not verified."** An unknown program is on port
  8000. Hina refuses to use its page for safety. Close that program and reopen Hina.
- **She does not hear me.** Check the system microphone permission and the device under Settings →
  Hearing. Hearing stays off until the key of the chosen engine (Groq by default; Deepgram,
  ElevenLabs Scribe or Gemini if you switched) is configured.
- **She answers "I don't know how to do that" to an action.** The agent is off or that tool is
  blocked under Dashboard → Agent.
- **Fallback voice instead of the chosen one.** The voice provider's credit ran out or the key is
  invalid; Hina retries in 10 minutes.
- **macOS says the app is damaged.** See [Install](#1-install): `xattr -cr`.
- **Another device on the network cannot connect.** By default Hina only answers on the same
  computer. Network access requires HTTPS and a token; it is an advanced setup outside this guide.

## 10. Privacy, license and contact

- [License](https://github.com/Project-H-I-N-A/hina-releases/blob/main/LICENSE): free for personal,
  non-commercial use; all rights reserved.
- [Privacy policy](https://github.com/Project-H-I-N-A/hina-releases/blob/main/PRIVACY.en.md).
- Bugs and questions: [hina-releases issues](https://github.com/Project-H-I-N-A/hina-releases/issues).
  Issues are public: never paste keys, personal data or conversation excerpts. Prefer attaching the
  *support bundle* (Dashboard → Settings → General → Support → *Download support bundle*), which already
  redacts secrets.
