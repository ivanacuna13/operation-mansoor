# Adobe bridge progress

Updated: 2026-09-08 (~14:55 PT / Europe/Lisbon)

## Implemented

- VM package: `tools/master-video-editor/adobe_bridge/` — package/submit/readback/disk_gate/batch_queue/mve_adobe/`mini_worker.py` + `premiere_startup_watcher.jsx`
- Submit race fix: `package.partial.json` → promote → `INCOMING.json`; worker claims only when both `package.json` + `INCOMING.json` exist
- Stale lock: dead-PID takeover (LaunchAgent no longer crash-loops on old lock)
- LaunchAgent `com.mansoor.mve.adobe-bridge`: **KeepAlive + RunAtLoad**, `ProcessType=Interactive`, domain **gui/501 Aqua**
- GUI-session Premiere path: cold `open -a --args /C es.processFile`, watch-folder drop under `premiere-watch/`, optional GUI direct binary (no SSH binary launch)
- GUI-session AME path: `ame-watch/inbox|outbox` + `open -a AME`; ffmpeg only as labeled fallback
- Stage 2 smoke: drops queue job for LaunchAgent — does **not** SSH-invoke Premiere/AME
- Docs: `AUTOMATION.md`, `stage2b_ivan_clicks.md`

## Proven (evidence under `adobe_bridge_evidence/`)

- **Stage 1 PASS**: SSH, versions, GUI user, echo queue
- **Stage 2b PARTIAL** (`stage2b_summary.json`, job `stage2-smoke-20260908T134602Z`):
  - LaunchAgent Aqua: **PASS** (no WebCrypto `-25308` on GUI Adobe launch)
  - Proxy: **PASS** `prores_videotoolbox`
  - Export: **PASS** hash only via `automation_path=ffmpeg_smoke_fallback` sha256 `24dc5f98951d8f95ff6207472b3d5a93cd6ae6a0ef40febf7d5e43cde91ae402`
  - Premiere `.prproj`: **FAIL** — cold-launch + GUI binary did not write marker
  - AME real export: **FAIL** — Watch Folder not enabled; webservice not live

## Blocked

1. **Premiere XML → versioned `.prproj`**: `/C es.processFile` does not complete JSX on Premiere 26.3.2 Mac even from Aqua. User Startup Scripts CC **not** loaded. App `Contents/Scripts/Startup/` needs `sudo cp` of `mve_queue_watcher.jsx` (Ivan one-time).
2. **AME export**: GUI `open -a` starts AME but does not encode without Watch Folder / webservice. Ivan must enable Watch Folder on `mve-adobe/ame-watch/inbox` → `outbox` with YouTube 720p HD.
3. Premiere AppleScript: **no DoScript** in sdef — cannot `osascript` inject ExtendScript.

## Remaining

1. Ivan: `sudo cp` Startup watcher into app Scripts/Startup; relaunch Premiere; confirm `premiere-watch/watcher_loaded.json`
2. Ivan: AME Watch Folder once (see `stage2b_ivan_clicks.md`)
3. Re-run Stage 2 smoke via queue drop; require `.prproj` + `automation_path=ame` for PASS
4. Optional later: CEP/UXP HTTP bridge if Startup+Watch Folder insufficient
5. Wire `readback.bind_revision_identity`; keep `upload_complete=false` until Frame

**Do not mark Stage 2 complete** until versioned `.prproj` + real AME (or proven Adobe) export hashes exist.
