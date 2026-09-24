# Premiere / AME automation surface (Mac Mini)

Measured against Premiere Pro 2026 26.3.2 + Media Encoder 2026 26.3.2 on ivanclawd Mini.
Layout: `/Users/ivanclawd/mve-adobe/` (queue/incoming → claimed → done|failed).
LaunchAgent: `com.mansoor.mve.adobe-bridge` in **Aqua `gui/501`** (KeepAlive + RunAtLoad).

## Present

| Surface | Status |
|---------|--------|
| ExtendScript framework | YES — `Contents/Frameworks/extendscript.framework` |
| App Startup JSX dir | YES — root-owned; custom watcher **not** installed (needs `sudo cp`) |
| User Startup Scripts CC | Installed `mve_queue_watcher.jsx` — **NOT loaded by Premiere 26** (measured) |
| CEP HtmlEngine | YES |
| UXP plugins | YES |
| AME webservice console | YES on disk — **not listening / not enabled** in smoke |
| ffmpeg videotoolbox | YES |
| osascript | binary present; Premiere sdef has **no DoScript** (only capture/editoriginal) |
| AppleScript remote AE | `com.apple.access_remote_ae` / ssh-disabled groups present |

## Preferred implemented path (GUI LaunchAgent only)

1. Submit writes `package.partial.json` → files → `package.json` + `INCOMING.json` (worker requires both — no race).
2. Worker (Aqua) stages sources, builds proxies (`prores_videotoolbox`).
3. Premiere: drop `premiere-watch/pending/<job>.run.json` + **cold** `open -a Premiere --args /C es.processFile <jsx>` (never pass `--args` to already-running app). Fallback: GUI-session direct binary. Startup watcher polls pending when installed in app `Scripts/Startup`.
4. AME: drop `ame-watch/inbox/`; `open -a AME`; poll outbox/exports. If no Adobe artifact → honest `ffmpeg_smoke_fallback` (never labeled AME).

## Stage 2b measured (2026-09-08 PT)

Evidence: `adobe_bridge_evidence/stage2b_summary.json` job `stage2-smoke-20260908T134602Z`.

| Check | Result |
|-------|--------|
| LaunchAgent Aqua session | PASS — `XPC_SERVICE_NAME=com.mansoor.mve.adobe-bridge`, no `-25308` |
| Proxy VT | PASS |
| Cold-launch `open -a --args /C es.processFile` | Premiere starts; **no JSX done marker / no .prproj** |
| GUI direct binary `/C es.processFile` | Timeout; internal connection refused; **no -25308** (session OK) |
| Startup watcher loaded | FAIL — `watcher_loaded.json` absent; pending jobs remain |
| AME GUI open + inbox drop | AME runs; **no encode artifact** without Watch Folder |
| Export hash | PASS via `ffmpeg_smoke_fallback` only |

## Ivan one-time clicks

See `adobe_bridge_evidence/stage2b_ivan_clicks.md`.

## Not ready

- Custom UXP/CEP HTTP `saveAs` + AME queue panel
- AME webservice authenticated submit
- Headless `.prproj` without Startup JSX in app bundle
