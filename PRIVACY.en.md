# Hina privacy policy

Last updated: October 2, 2026 · [Português](PRIVACY.md)

## In one sentence

Hina runs on your computer. What leaves it is what you send to the AI providers you set up with your
own keys, plus the little the app needs to open the avatar and check for updates. There is no Hina
server receiving your data.

## 1. Who is responsible

Hina is maintained by **Project H.I.N.A.** and is free software (GPLv3). It has no user account,
asks for no sign-up and charges nothing: the API keys are yours, and each provider bills you
directly.

Contact: open an issue at
[github.com/Project-H-I-N-A/hina-releases/issues](https://github.com/Project-H-I-N-A/hina-releases/issues).
Issues are public: do not put personal data, API keys or parts of your conversations in them.

## 2. What stays on your computer only

All of this lives in the app's data folder and is never sent anywhere by Hina:

- **Windows:** `%APPDATA%\Hina`
- **macOS:** `~/Library/Application Support/Hina`
- **Linux:** `~/.config/Hina`

What is kept there:

- **Conversation memory:** history, facts she keeps about you and the search index, one database per
  avatar + persona pair. You can see, edit and delete all of it in the Dashboard's Memory tab.
- **Personality:** the style profile that evolves with use.
- **Usage telemetry:** response time, tokens and estimated cost of each turn, so the Dashboard can
  show your spending. It stays in a local database and can be turned off in Settings.
- **Server log** (`logs/server.log`): technical messages, which may quote parts of what you said.
- **Your API keys:** in the system vault (Credential Manager on Windows, Keychain on macOS, Secret
  Service on Linux). The installed app never writes keys as plain text.
- **Interface settings and preferences.**

Uninstalling the app **does not delete** that folder. To remove everything, delete the folder after
uninstalling.

## 3. What leaves your computer, and to whom

Hina only sends data to services you chose and set up with your own key, with one exception (the
fallback voice, below). Each service has its own privacy policy and retention rules; Hina does not
control what they do with what they receive.

| What is sent | Where to | When |
|---|---|---|
| The conversation text: what you type or say, plus the memory context Hina attaches | The language provider chosen in Settings. Default: Google Gemini. Alternatives: Groq, OpenAI, xAI and OpenRouter | Every conversation turn |
| Your microphone audio | The speech recognition provider: Deepgram (default), Groq Whisper (without a Deepgram key) or Google (Live mode) | Only while listening is on (microphone button or push-to-talk) |
| The text of the replies, to turn into voice | ElevenLabs (default), Google Gemini or Cartesia. **With no voice key at all**, Microsoft's free edge-tts service (`speech.platform.bing.com`) | Every spoken reply. The fallback voice works even if you set nothing up |
| Screenshots of your screen | The vision model (default: Google Gemini) | Only when you turn on screen viewing in the pet menu or "Continuous screen perception" (off by default). The "Hide secrets seen on screen (privacy)" option tries to remove passwords and keys before sending, with no guarantee |
| Computer audio (what is playing) | The speech provider or, if you turn on music identification, ACRCloud | Only while PC audio listening is on (pet menu) |
| Camera images | **Nobody.** Face tracking runs inside the app (MediaPipe) | Only with "Face tracking" on. The model files are downloaded from `cdn.jsdelivr.net` and `storage.googleapis.com` the first time |
| File contents, command output and pages read by the agent | The language provider | When you ask the agent to act. Tools that write, delete or run something ask for your confirmation unless you tick "always allow" |
| Connector data (calendar, e-mail, Spotify, Telegram, Discord) | The language provider and the connected service itself | Only if you connect the service in the Dashboard |
| The whole conversation | Hermes Agent, if you install and turn it on, and from there the provider set in its profile | Only in Hermes mode. Hina's memory and learning are paused in that mode |
| Latency metrics (times and sizes, no text) | Langfuse | Only if you set up Langfuse keys and turn sending on |

## 4. Connections the app makes on its own

Even with no keys at all, the installed app makes these requests:

- **`cubism.live2d.com`:** the Live2D core, loaded every time the window opens. It is not bundled in
  the installer because of its license.
- **`cdn.jsdelivr.net`:** the Spine avatar library, only if you use a Spine avatar.
- **`github.com`:** about 30 seconds after opening, Hina checks for a new version at
  `Project-H-I-N-A/hina-releases`. None of your data goes with that check, and an update is only
  downloaded and installed if you confirm.
- **`speech.platform.bing.com`:** Microsoft's fallback voice, only when there is no voice key.

## 5. Local network and sync

Hina only accepts connections from the computer itself (`127.0.0.1`). Local network access and sync
between computers are off and have no interface; turning them on requires editing the configuration
and setting a token.

## 6. Support bundle

Settings has "Download support bundle": a zip with version, system, providers, flags, the
configuration with key values removed and the end of the server log. It is only created when you
click, and only goes where you send it. The log may quote parts of the conversation: review it
before sending.

## 7. Your controls

- **Delete memory, facts and history:** Dashboard, Memory tab.
- **Turn off telemetry, vision, listening, PC audio and face tracking:** Settings and the pet menu.
- **Change or remove keys:** Settings. Removing a key turns the matching service off.
- **Delete everything:** uninstall, remove the data folder (§2) and delete Hina's entries from the
  system vault.

## 8. What Hina does not do

It has no account or analytics of its own, sends no automatic error reports, does not sell or share
data and does not use your data to train anything. Whether a provider uses what it receives to train
models is that provider's rule and depends on the plan you have with it (free plans often allow it).
Check the policy of each provider you set up.

## 9. Changes to this policy

Every change is listed in the release notes of the version that brings it, and the new text applies
from that version on. The date at the top of this file shows the last update.
