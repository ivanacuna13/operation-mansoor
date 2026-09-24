# Premiere / AME bridge

Status: **OPERATIONAL PARTIAL** (Stage 2b measured 2026-09-08 ~14:55 PT) — GUI LaunchAgent OK; `.prproj`/AME still blocked pending Ivan one-time clicks.

## Verified Mini

- Premiere Pro 2026 → `/Applications/Adobe Premiere Pro 2026/Adobe Premiere Pro 2026.app` (26.3.2)
- Media Encoder 2026 → `/Applications/Adobe Media Encoder 2026/Adobe Media Encoder 2026.app` (26.3.2)
- Photoshop 2026 → 27.10.0
- GUI console: `ivanclawd`
- SSH: `ssh -F /home/box/.ssh/mini_cfg mini`
- Layout: `/Users/ivanclawd/mve-adobe/` (`queue/incoming|claimed|done|failed`, `staging/{sources,proxies,tmp}`, `projects`, `exports`, `worker/{bin,logs,locks}`, `tools/*` symlinks)
- VM pair: `/home/box/mansoor-content-operations/adobe-bridge/`
- Code package: `tools/master-video-editor/adobe_bridge/`

## Stage results

| Stage | Result | Evidence |
|-------|--------|----------|
| 1 SSH + versions + echo queue | **PASS** | `adobe_bridge_evidence/stage1_*.json` |
| 2 synthetic → proxy → export hash | **PARTIAL** | `adobe_bridge_evidence/stage2_summary.json` |
| 2 Premiere XML→versioned `.prproj` | **BLOCKED** | Aqua cold-launch + GUI binary: no JSX marker; Startup watcher needs `sudo cp` into app Scripts/Startup (`stage2b_ivan_clicks.md`) |
| 2 AME CLI export | **BLOCKED** | GUI `open -a` starts AME; no encode without Watch Folder; webservice not live |
| 2 farthest safe export | **PASS** (honest fallback) | `ffmpeg h264_videotoolbox` → `exports/<job>/…mp4` + sha256; labeled `automation_path=ffmpeg_smoke_fallback` |
| 2 proxy | **PASS** | `prores_videotoolbox` 960x540 → `staging/proxies/<job>/` |

## Automation surface (see `adobe_bridge/AUTOMATION.md`)

Present on disk: ExtendScript.framework, CEP, UXP, AME webservice console, ffmpeg VT.
**Not proven headless:** JSX `es.processFile` save, AME CLI encode, UXP panel bridge.
Prefer next: CEP/UXP HTTP bridge or AME watch-folder with GUI session — not UI AX without Accessibility grant.

VM = manifests / Astra / identity / Frame / QC. Mini = Adobe+GPU worker. No Frame uploads in bridge smoke.
