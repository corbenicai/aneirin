# Aneirin for Windows — getting started

Aneirin is a single program: `aneirin.exe`. No install of Node or anything else is needed.

> First run shows a "Windows protected your PC / unknown publisher" prompt until the build
> is code-signed. Click **More info → Run anyway**. (A signed build removes this.)

## 1. Put it somewhere and check it
Unzip, then in a terminal (PowerShell) in the unzipped folder:
```
.\aneirin.exe selftest
```
You should see **`Aneirin engine OK`**.

## 2. Trust the local certificate (one time)
Aneirin optimizes HTTPS traffic on your own machine, so it needs a local certificate it
generates *on your computer* (never shipped, unique to you):
```
.\aneirin.exe install-ca
```

## 3. Start Aneirin
```
.\aneirin.exe
```
This runs the local optimizer on `127.0.0.1:8765`. Leave it running. (Stop it with Ctrl+C.)

## 4. Send your AI tool's traffic through it
- **Claude Code (CLI):** set the proxy for the session, then use Claude Code as normal:
  ```
  $env:HTTPS_PROXY = "http://127.0.0.1:8765"
  ```
- **VS Code:** the Aneirin extension (coming next) wires this up automatically.

That's it. You're on the **Free** tier (full optimizer, 5,000,000 optimized tokens/day).
Watch your savings in the dashboard / ledger inside your Aneirin folder.

## 5. Activate a licence (optional)
After buying, paste your token:
```
.\aneirin.exe activate "PASTE-YOUR-TOKEN-HERE"
```
Your device code (for checkout) is shown by:
```
.\aneirin.exe activate
```

## Remove it
```
.\aneirin.exe uninstall      # removes the local CA trust + restores normal traffic
```
Then delete the folder. Aneirin makes no system changes beyond the local certificate it
removes here.

---
*Privacy: see PRIVACY.md. What it does and the responsibilities involved: see RISK.md.*
