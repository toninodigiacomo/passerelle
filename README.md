# Passerelle
A Claude-style chat interface, in a **single HTML file**, requiring no server or installation. 
It queries multiple AIs in an order of priority that you define (free ones first, paid ones as a last resort) and keeps a secure history on your hard drive, organized by day and by conversation.

Designed for users without admin privileges: just open `passerelle.html` in the browser—that’s it.

## Features
- **No installation** — a single HTML file, opened directly in the browser.
- **Multiple providers** — Claude, Gemini, Mistral, ChatGPT (OpenAI).
- **Reorderable priority** — put free AI models first, paid ones as a backup.
- **Incognito mode** — controls what is displayed and reloaded on startup (enabled by default).
- **Disk backup, always active** — whether in incognito mode or not, each conversation is saved to the folder of your choice, with one folder per day and one file per conversation
- **Configuration can be exported/imported as XML**, in addition to automatic backup in the browser

## Getting Started
1. Clone the repository (`git clone` or download the ZIP file)
2. Open `index.html` in **Chrome** or **Edge** (double-click or drag and drop it into the browser)
3. Click the settings icon (gear, top right) and enter at least one API key

No commands, no servers, no dependencies to install.

## Settings
Open the settings panel to:

| Section | Function |
|---|---|
| **Privacy** | Enables/disables incognito mode and allows you to clear the displayed history |
| **Backup Folder** | *Browse…* button to choose where to save conversations on disk |
| **Priority Order** | ↑/↓ arrows to set which provider is tried first, and a toggle to enable/disable it |
| **Gemini / Mistral / ChatGPT / Claude** | API key and model for each provider |
| **Configuration file** | Export/import configuration in XML format |

### Get an API key
- **Claude** — [console.anthropic.com](https://console.anthropic.com) (paid)
- **Gemini** — [aistudio.google.com/apikey](https://aistudio.google.com/apikey) (generous free tier)
- **Mistral** — [console.mistral.ai](https://console.mistral.ai) (free tier with data limits)
- **OpenAI (ChatGPT)** — [platform.openai.com](https://platform.openai.com) (paid, no permanent free tier)

## Backup Configuration
Once a folder is configured, a file is created for each conversation within a daily subfolder:
```txt
[selected folder]/
├── 2026-09-09/
│   ├── conversation-09h14-a1b2.jsonl
│   └── conversation-14h32-f3d8.jsonl
└── 2026-09-10/
    └── conversation-08h50-7e1a.jsonl
```
Each line of the `.jsonl` file is a message in JSON format (one object per line), which allows to add content without having to rewrite the entire file for each message.  
A new conversation begins when you open the page or by clicking the “New Conversation” icon in the banner.

## Browser Compatibility
Saving to disk uses the *File System Access API*, which is available only on **Chrome and Edge** (not yet on Firefox or Safari). 
Without this API, the app works normally but does not automatically save to disk—in that case, be sure to use the XML export/import feature to preserve your settings.
The browser will ask for permission to access the folder again at the start of each new session: this is normal security behavior, not a bug.

## Security and Privacy
- API keys are stored **locally in the browser**
  (`localStorage`) and are never transmitted anywhere other than to the relevant providers (Anthropic, Google, Mistral, OpenAI).
- Each request is made **directly from the browser** to the provider’s API. There is no intermediary server.
- Avoid using this file on a shared computer, or be sure to clear your browser’s local storage after use.
- Never add a real API key to this Git repository!

## Known Limitations
- Direct calls from the browser to the OpenAI and Mistral APIs are not officially supported (CORS).
- Claude and Gemini are documented for this use.
- On a corporate network with a strict proxy or firewall, calls to  the APIs may be blocked.
- No offline support: an internet connection is required.

## Licence
GNU GPL v3.0 - [LICENCE.md](https://github.com/toninodigiacomo/passerelle/blob/316d072f3c527e1a7c5377629cd70bd960efb542/LICENSE.md)
