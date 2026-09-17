# Tab Resource Monitor — native helper

Public installers for the **Tab Resource Monitor** Chrome extension's local
native helper. The extension is sandboxed and can't read true CPU/RAM or run
programs, so a tiny local process (a Chrome *native messaging host*) provides:

- accurate **system CPU%** and memory,
- Chrome's **true footprint** and a real per-process breakdown (matches Activity
  Monitor / Task Manager) on every Chrome channel,
- optionally, **every tab across all windows and profiles** (when Chrome runs
  with a remote-debugging port).

Everything runs locally; nothing is sent anywhere.

## Install (one command)

Requires [Node.js](https://nodejs.org). The script is self-contained — it writes
the helper to `~/.tab-resource-monitor` and registers it for every installed
Chromium browser (Chrome, Chromium, Brave, Edge). No arguments: the extension ID
is pinned in the extension's manifest.

- **macOS / Linux**
  ```bash
  curl -fsSL https://raw.githubusercontent.com/yuriiluchyshyn/tab-resource-monitor/main/bootstrap.sh | bash
  ```
- **Windows** (PowerShell)
  ```powershell
  irm https://raw.githubusercontent.com/yuriiluchyshyn/tab-resource-monitor/main/bootstrap.ps1 | iex
  ```

Then open the monitor (or press **Re-check** on the extension's setup page) — its status line should read `native: on`.

## See tabs from all windows & profiles (optional)

Start Chrome with a debugging port, then set that port in the extension's
Options:

```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
```

A debugging port lets any local program control that Chrome — enable it only
when you need the cross-profile view.

## Uninstall

```bash
rm -rf ~/.tab-resource-monitor
```

Then delete `com.billing.tabmonitor.json` from each browser's
`NativeMessagingHosts` folder (Windows: remove the `com.billing.tabmonitor`
registry key under each browser's `NativeMessagingHosts`).

## What's here

| File | Purpose |
| --- | --- |
| `bootstrap.sh` | One-command installer for macOS / Linux (embeds the host). |
| `bootstrap.ps1` | One-command installer for Windows (embeds the host). |

These files are generated from `host.js` in the extension source
(`build-bootstrap.js`); edit them there, not here.
