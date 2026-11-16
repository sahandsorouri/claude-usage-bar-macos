<img src="https://raw.githubusercontent.com/sahandsorouri/sahandsorouri/main/assets/banner.svg" alt="Sahand Sorouri" width="100%">

# Claude Usage Bar

A small macOS menu bar app that shows your claude.ai usage limits (the 5-hour session and the weekly limit) at a glance.

## What it does

- Shows the same numbers as the claude.ai usage settings page, with no calibration.
- Menu bar modes: a colored ring (green up to 50%, orange 51 to 74%, red from 75%), a percent, session and weekly together, or percent with time left.
- The dropdown always lists session and weekly details.
- Sends a macOS notification when your 5-hour or weekly window resets.
- Talks only to claude.ai. No Dock icon.

## Install

1. Download `Claude-Usage-Bar.dmg` from [Releases](https://github.com/sahandsorouri/claude-usage-bar-macos/releases) and open it.
2. Drag **Claude Usage Bar** to **Applications**.
3. The app is unsigned, so the first launch needs a right-click on the app, then **Open**, then **Open** again.
4. The icon appears in the menu bar.

Needs macOS 11 or later. Works on Apple Silicon and Intel.

## First run and login

On first launch a **Sign in to Claude** window opens. Log in with your normal Claude account; the window closes and your usage appears.

- Only the claude.ai session cookie is kept, in `~/Library/Application Support/ClaudeUsageBar/session.json` (readable only by you).
- No macOS Keychain and no system password prompts.
- To sign in again later: **menu > Account > Log in to Claude...**
- Optional: **menu > Account > Use Brave cookies** imports the session from a logged-in Brave profile. Off by default.

See [`AUTH.md`](AUTH.md) for the full design.

## Build from source

Needs Python 3.11.

```bash
pip3.11 install -r requirements.txt

python3.11 claude_usage_bar.py   # run from source
bash scripts/build_app.sh        # build the .app
bash scripts/build_dmg.sh        # build dist/Claude-Usage-Bar.dmg
python3.11 make_icon.py          # regenerate AppIcon.icns
```

The build bundles its dependencies but still uses the system Python framework. Signing and notarizing are not done yet; see [`ROADMAP.md`](ROADMAP.md).

## Troubleshooting

- **"App is damaged" or "can't be opened":** right-click the app and choose Open, or run `xattr -cr "/Applications/Claude Usage Bar.app"`.
- **Bar shows `!`:** a fetch failed (offline, or the session expired). Try **Account > Log in to Claude...**
- **Bar shows `Log in`:** no saved session yet. Open the login window from the Account menu.

## Project layout

| Path | Purpose |
|------|---------|
| `claude_usage_bar.py` | The menu bar app (rumps) |
| `auth_session.py` | Session storage and the login window |
| `make_icon.py` | Generates `AppIcon.icns` |
| `setup.py` | py2app build config |
| `scripts/` | Build scripts for the `.app` and the `.dmg` |
| `legacy/` | An older, unrelated Telegram bot, kept for reference only |

## Tech

Python 3.11, rumps, WKWebView (PyObjC), py2app.

---

Built by [Sahand Sorouri](https://sahand.sorouri.com) · platforms, bots and AI tools for businesses in Dubai.
