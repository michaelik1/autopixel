# AutoPixel

**Pixel Google One Assistant**

AutoPixel is a Telegram bot that simulates a Pixel device session (Pixel 11 Pro on Android 17 by default, with the Google AI Pro-eligible Pixel 9 Pro and Pixel 10 Pro lineup also available), signs in to a Google account, checks Google One / Google AI Pro offer availability, and gives you a modern control panel for session, proxy, IP, and diagnostic tools.

## Highlights

- Simulates a fresh Pixel device profile for each login session (defaults to Pixel 11 Pro on Android 17)
- Switchable device profiles for the Google AI Pro-eligible Pixel lineup (Pixel 9 Pro / 9 Pro XL / 9 Pro Fold, Pixel 10 Pro / 10 Pro XL / 10 Pro Fold, and Pixel 11 Pro) via `DEVICE_PROFILE` or the per-user `/device` picker
- Supports Gmail and Google Workspace accounts
- Handles Google sign-in with TOTP / authenticator flow support
- Can attempt audio captcha solving through `wit.ai` before falling back to manual verification
- Checks Google One pages for Google AI Pro offer availability
- Supports proxy pool rotation and direct/local IP mode
- Shows public IP, region, ZIP, org, ISP, ASN, timezone, and other proxy identity details
- Saves screenshot + HTML debug artifacts when no offer is found
- Supports English and Indonesian UI
- Ships with a modern Telegram dashboard:
  - header media
  - 2-column grid buttons
  - `[·]` section cards
  - emoji-rich menu labels

## Latest Product Update

As of **November 26, 2026**, the current user-facing baseline includes:

- **Pixel 11 Pro on Android 17** is now the default simulated device, with Pixel 11 Pro `grizzly` build IDs, a 1280 × 2856 panel, a 410 × 914 CSS viewport at DPR 3.125, Tensor G6 core count, PowerVR CXTP-48-1536 WebGL identity, and Android 17 Client Hints
- device-aware Google AI Pro offer messaging: the Pixel 11 Pro profile shows the current **6-month / 5 TB** trial, while the Pixel 9/10 Pro profiles keep the older **12-month / 2 TB** terms
- 6-month and 5 TB offer markers in the Google One scanner so the current Pixel 11 Pro promo is diagnosed and captured correctly
- the per-user `/device` picker still lets each Telegram chat switch profiles without restarting the bot

Earlier onboarding improvements remain in place: `/doctor`, `.env`-ready `/ip` output, safer numeric fallbacks, and the tracked sample `proxies.txt`.

## Documentation

| File | Purpose |
|---|---|
| `README.md` | Product overview, setup summary, commands, and troubleshooting |
| `HOW TO RUN IT .txt` | Plain-text run guide for Windows PowerShell, Windows CMD, and Android Termux |
| `CHANGELOG.md` | Baseline release notes and architecture history |

## Pixel Promo Matrix

As of **November 26, 2026**, Google's official Pixel offer page lists these Google AI Pro trials for current and recent Pixel Pro devices:

| Device family | Service | Trial length | Storage | Offer expires |
|---|---|---|---|---|
| Pixel 11 Pro / 11 Pro XL / 11 Pro Fold | Google AI Pro | 6 months | 5 TB | October 31, 2027 |
| Pixel 10 Pro / 10 Pro XL / 10 Pro Fold | Google AI Pro | 12 months (6 months in Japan) | 2 TB | October 31, 2026 |
| Pixel 9 Pro / 9 Pro XL / 9 Pro Fold | Google AI Pro | 12 months (6 months in Japan) | 2 TB | November 15, 2025 |
| Pixel 11 (base model) | — | No Google AI Pro trial | — | — |

Important notes:

- The Pixel 11 Pro terms page lists a broad country set, including the United States, Canada, the United Kingdom, EU countries, India, Japan, Australia, and more. Check the official terms page for the full list before relying on a specific country.
- The older Pixel 10 Pro and Pixel 9 Pro promos have already expired; the Pixel 11 Pro offer is the current one in this matrix.
- Google's Pixel 11 Pro redemption instructions are app-based (Gemini or Google One app). AutoPixel checks the web Google One pages, so an eligible account may still need to redeem from the phone app if no web link is captured.
- Google AI Pro itself is supported in a much wider set of countries and regions than the Pixel-device promo. That means the plan may exist in a country even when the Pixel promo is not officially listed there.
- Actual eligibility still depends on device purchase + activation, account status, billing profile, and Google's live eligibility checks.
- This bot can only check for offer visibility and eligibility. It cannot make an account eligible in a country or billing profile that Google does not support.

Official sources:

- [Google One offers for Pixel devices](https://support.google.com/pixelphone/answer/13529884?hl=en-GB)
- [Pixel 11 Pro Google One offer terms](https://one.google.com/offer/terms-and-conditions/pixel11pro)
- [Get a Google AI Pro membership](https://support.google.com/googleone/answer/16476811?co=GENIE.Platform%3DDesktop&hl=en)

## Main Commands

| Command | Function |
|---|---|
| `/start` | Open the Pixel Control Panel |
| `/doctor` | Run a first-time setup self-check |
| `/login` | Save Google email + password and create a fresh device session |
| `/witai` | Save or clear the Wit.ai token used for audio captcha solving |
| `/check_offer` | Start login automation and scan Google One for an offer |
| `/get_link` | Show the last captured offer link |
| `/status` | Show account, proxy, and device session info |
| `/proxy` | Show the active proxy and proxy pool status |
| `/ip` | Show public IP and geo/identity data |
| `/rotate_proxy` | Switch to another proxy from the pool |
| `/disable_proxy` | Force the session to use direct/local IP |
| `/device` | Pick which Pixel device the bot simulates for your chat |
| `/lang_en` | Switch bot UI to English |
| `/lang_id` | Switch bot UI to Indonesian |
| `/langid` | Alias for `/lang_id` |
| `/logout` | Clear active session, credentials, and temporary browser state |
| `/cancel` | Cancel the current login / verification flow |

## Current UI

The bot now uses:

- a modern welcome card
- a local banner/header image on `/start`
- a 2-column inline control panel
- reply-keyboard navigation buttons

Important: old inline panels sent before the latest update still contain the old non-working inline-query buttons. Send `/start` again to get the new working control panel.

## Project Structure

```text
AUTOPIXEL/
├── main.py
├── config.py
├── requirements.txt
├── README.md
├── core/
│   ├── proxy_manager.py
│   └── session_manager.py
├── handlers/
│   ├── auth_handlers.py
│   ├── device_handlers.py
│   ├── offer_handlers.py
│   ├── session_handlers.py
│   └── ui.py
├── services/
│   ├── device_simulator.py
│   ├── google_automation.py
│   └── network_diagnostics.py
└── assets/
    └── telegram/
        └── pixel-header.png
```

## Requirements

- Python 3.10+
- Google Chrome installed
- A Telegram bot token from `@BotFather`
- Internet connection
- Optional: `proxies.txt` if you want proxy mode
- Full browser automation is best supported on Windows, Linux, or macOS with desktop Chrome available

## Quick Start

For the full plain-text run guide, see [`HOW TO RUN IT .txt`](HOW%20TO%20RUN%20IT%20.txt).

After the bot starts for the first time, run `/doctor` in Telegram to verify token, Chrome detection, header media, proxy pool readiness, and driver configuration before testing a real account.

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
Copy-Item .env.example .env
.\.venv\Scripts\python.exe main.py
```

### Windows Command Prompt (CMD)

```bat
python -m venv .venv
.venv\Scripts\activate.bat
python -m pip install --upgrade pip
pip install -r requirements.txt
copy .env.example .env
.\.venv\Scripts\python.exe main.py
```

### Android Termux

```bash
pkg update && pkg upgrade -y
pkg install -y python git clang rust libffi openssl
cd /path/to/AUTOPIXEL
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip setuptools wheel
pip install -r requirements.txt
cp .env.example .env
python main.py
```

Termux note: the Telegram bot process can run in Termux, but Chrome-based Google login automation normally requires a desktop-class Chrome/WebDriver environment.

## Detailed Setup Notes

### Environment file

Copy `.env.example` to `.env` and fill what you need:

```env
TELEGRAM_BOT_TOKEN=YOUR_BOT_TOKEN
BOT_HEADER_MEDIA_URL=
CHROME_BIN=
CHROMEDRIVER_PATH=
GOOGLE_CAPTCHA_AUTO_SOLVE=1
WIT_AI_TOKEN=
PROXY_ENABLED=1
PROXY_FILE_PATH=
PROXY_FAILURE_COOLDOWN_SECONDS=90
PROXY_QUARANTINE_SECONDS=300
PROXY_QUARANTINE_THRESHOLD=3
PROXY_DIAGNOSTICS_VERIFY_SSL=0
```

Notes:

- `BOT_HEADER_MEDIA_URL` supports a local image path, image URL, GIF URL, or MP4 URL
- if `BOT_HEADER_MEDIA_URL` is empty, the bot uses the bundled local banner asset
- if `CHROMEDRIVER_PATH` is empty, the runtime falls back to automatic driver resolution
- you can also set the Wit.ai token from Telegram with `/witai` and the bot will store it in `.env`
- set `WIT_AI_TOKEN` if you want AutoPixel to try solving audio captcha challenges automatically
- if you need help getting a Wit.ai token, see `HOW TO GET A WIT.AI API KEY.txt`
- `PROXY_DIAGNOSTICS_VERIFY_SSL=0` lets `/ip` and proxy precheck tolerate self-signed/intercepted TLS chains often seen on proxy routes

### Optional device profile

AutoPixel defaults to a **Pixel 11 Pro on Android 17** profile. Only Pixel devices with a Google AI Pro trial offer (current or historical) are bundled — that means the Pixel 9 Pro / 9 Pro XL / 9 Pro Fold, the Pixel 10 Pro / 10 Pro XL / 10 Pro Fold, and the Pixel 11 Pro. To switch to another preset, set it in `.env`:

```env
DEVICE_PROFILE=pixel_10_pro
```

Available presets:

| Preset | Device | Android | SDK | GPU | RAM | AI Pro trial |
|---|---|---|---|---|---|---|
| `pixel_11_pro` (default) | Pixel 11 Pro | 17 | 37 | PowerVR CXTP-48-1536 MC1 | 12 GB | 6 months / 5 TB |
| `pixel_10_pro` | Pixel 10 Pro | 16 | 36 | Adreno 750 | 12 GB | 12 months / 2 TB |
| `pixel_10_pro_xl` | Pixel 10 Pro XL | 16 | 36 | Adreno 750 | 16 GB | 12 months / 2 TB |
| `pixel_10_pro_fold` | Pixel 10 Pro Fold | 16 | 36 | Adreno 750 | 16 GB | 12 months / 2 TB |
| `pixel_9_pro` | Pixel 9 Pro | 16 | 36 | Mali-G715 Immortalis MP7 | 16 GB | 12 months / 2 TB |
| `pixel_9_pro_xl` | Pixel 9 Pro XL | 16 | 36 | Mali-G715 Immortalis MP7 | 16 GB | 12 months / 2 TB |
| `pixel_9_pro_fold` | Pixel 9 Pro Fold | 16 | 36 | Mali-G715 Immortalis MP7 | 16 GB | 12 months / 2 TB |

RAM is the physical device RAM. Chrome reports `navigator.deviceMemory` as `8` on Android even for 12 GB phones because Chrome clamps that API to 8, and the Pixel 11 Pro profile follows that behavior. The Tensor G6 is a 7-core CPU, so the profile also reports `navigator.hardwareConcurrency = 7`.

Only the Pixel 11 Pro is bundled from the Pixel 11 generation; Pixel 11 Pro XL and Pixel 11 Pro Fold presets are not included yet.

Switching the profile changes the simulated user-agent, Pixel codename fingerprint, build IDs, screen metrics, WebGL renderer, RAM/core hints, Client Hints headers, and offer messaging so the session matches the chosen device. An unknown value logs a warning and falls back to the default Pixel 11 Pro / Android 17 profile.

`DEVICE_PROFILE` only sets the **default** for new chats. From inside Telegram you can override it per user without restarting the bot:

- send `/device` (or tap the **📱 Pick Device** button on the Control Panel)
- pick any preset from the inline keyboard
- the bot stores the choice in your chat session and applies it next time a fresh device profile is generated (e.g. on `/login`, `/check_offer`, `/rotate_proxy`, `/disable_proxy`)
- if there is already an active session, the device profile is rebuilt in place so the change takes effect immediately

### Optional proxies

The repository includes a sample `proxies.txt` in the project root.
Edit that file directly if you want proxy mode.

If you want the bot to start in direct mode by default, set `PROXY_ENABLED=0`.
Leaving `PROXY_FILE_PATH` empty does not disable proxy mode. It only falls back to the default `proxies.txt` path.

Supported formats:

```text
http://ip:port
http://user:pass@ip:port
https://user:pass@ip:port
socks5://ip:port
ip:port:user:pass
user:pass@ip:port
```

## Typical Flow

1. Send `/start`
2. Send `/doctor` to validate first-run setup
3. Send `/lang_id` if you want Indonesian UI
4. Send `/login`
5. Enter email
6. Enter password, or `password|totp_secret`
7. Check `/ip` or `/proxy`
8. Send `/check_offer`
9. If 2FA is requested, send the 6-digit code in Telegram
10. Review the result or debug artifacts

## Success Example

This is a simple example so users can recognize a normal successful flow:

```text
You: /start
Bot: Pixel Control Panel opens

You: /login
Bot: Please enter your Google email address

You: user@gmail.com
Bot: Email accepted. Now send your password

You: yourpassword
Bot: ✅ Session Ready
Bot: A fresh Pixel device profile is ready for this session

You: /check_offer
Bot: ⏳ Starting secure check...
Bot: 🌍 Active Proxy Panel ...
Bot: ✅ Login successful
Bot: 🎉 Google AI Pro Offer Found! 🔗 https://one.google.com/...
```

## How Users Know It Worked

- Login step is successful when the bot shows `✅ Session Ready`
- Proxy/direct check is successful when `/ip` or `/proxy` shows the active network identity
- Offer check is successful when the bot shows `🎉 Google AI Pro Offer Found!`
- If no offer exists, the bot will say no active offer was found and may attach screenshot/HTML debug artifacts

## Proxy and IP Notes

- `/proxy` shows the active proxy for the session and pool availability
- `/ip` shows the effective network identity
- `/disable_proxy` locks the session to direct/local IP
- `/rotate_proxy` re-enables proxy mode for the session and chooses another proxy
- when proxy transport fails, `/check_offer` can rotate automatically

## Debug Artifacts

When no offer is found, the bot can save:

- screenshot `.png`
- page source `.html`

Artifacts are stored under:

```text
logs/offer_debug/chat_<chat_id>/
```

This helps distinguish:

- no eligible promo
- regular paid Google AI Pro plan only
- page rendering or scanner mismatch

## BotFather Copy

### Short Description

```text
Pixel 11 Pro Google One assistant with login automation, proxy tools, IP diagnostics, and Google AI Pro offer checking.
```

### Description

```text
This bot helps you manage secure Google One / Google AI Pro offer checks with a modern Pixel-style control panel.

✅ Secure Login: Save a session and launch Google sign-in safely
✅ Offer Check: Scan Google One pages for Google AI Pro offer availability
✅ Proxy Tools: Rotate proxy, disable proxy, or inspect IP identity in real time
✅ Session Status: Review account, device, and connection details instantly

Tap /start to open the Pixel Control Panel.
```

## Security Notes

- Credentials are kept in memory for the active session only
- Passwords are wiped after use in the offer-check flow
- Sessions expire automatically after the configured TTL
- Automation may still trigger Google security challenges depending on account risk and region context

## Troubleshooting

| Issue | Fix |
|---|---|
| You are not sure whether the bot is ready for first-time use | Run `/doctor` in Telegram and fix any warning before testing a real account |
| `No module named 'telegram'` or another missing package | Activate `.venv`, then run `pip install -r requirements.txt` again |
| `409 Conflict` | Stop duplicate `main.py` bot processes and restart one instance only |
| `/check_offer` says no credentials | Run `/login` again because the session password has already been cleared |
| Google gets stuck on an audio captcha | Set `WIT_AI_TOKEN` in `.env` so AutoPixel can try the audio challenge automatically, or finish it manually in Chrome |
| Proxy is selected but traffic still looks direct, or proxy precheck fails | Check `/proxy` and `/ip`, then rotate or replace the proxy pool, or switch to direct mode |
| No offer found on the Pixel 11 Pro profile | Confirm the account is eligible for the current 6-month / 5 TB Google AI Pro trial and has not already redeemed it. The older Pixel 10 Pro 12-month / 2 TB promo ended October 31, 2026 |
| No offer found | Review account region, billing profile, payments setup, and whether the promo was already claimed |
| Termux runs the bot but browser automation fails | Use Windows, Linux, or macOS with desktop Chrome for full automation support |

## Disclaimer

Use this project responsibly and only with accounts you own or are authorized to use. Automation against third-party services may be restricted by their policies or terms.
