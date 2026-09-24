# Ivan one-time GUI clicks (Mac Mini) — Stage 2 unblock

Measured 2026-09-08 PT. LaunchAgent `com.mansoor.mve.adobe-bridge` runs in Aqua `gui/501`.
Keychain `-25308` is fixed for GUI-launched Adobe. Remaining blockers need console clicks.

## 1) Premiere Startup watcher (required for `.prproj`)

`es.processFile` via `open -a --args` and GUI direct binary does **not** write JSX markers on Premiere 26.3.2.
User `~/Library/.../Startup Scripts CC/` is **not** loaded by Premiere.

**Do once (admin password):**

```bash
sudo cp /Users/ivanclawd/mve-adobe/premiere-watch/mve_queue_watcher.jsx \
  "/Applications/Adobe Premiere Pro 2026/Adobe Premiere Pro 2026.app/Contents/Scripts/Startup/90_mve_queue_watcher.jsx"
```

Then quit Premiere fully and reopen once. Confirm:

```bash
cat /Users/ivanclawd/mve-adobe/premiere-watch/watcher_loaded.json
```

## 2) AME Watch Folder (required for real AME export)

`open -a AME <media>` does not auto-encode. Webservice console present but not listening/authenticated.

**Do once in AME GUI:**

1. Open **Adobe Media Encoder 2026**
2. Enable **Watch Folders**
3. Add inbox: `/Users/ivanclawd/mve-adobe/ame-watch/inbox`
4. Output: `/Users/ivanclawd/mve-adobe/ame-watch/outbox`
5. Preset: **YouTube 720p HD** (system `.epr`)
6. Leave AME running in the GUI session (LaunchAgent will `open -a` it)

## 3) Optional

- System Settings → Privacy → Accessibility: allow `osascript` / Terminal if we later use UI scripting (not required for Startup+Watch Folder path)
- Do **not** tccutil reset

After both clicks, re-drop a Stage 2 smoke package into `queue/incoming` (LaunchAgent claims it). PASS needs versioned `.prproj` + AME artifact hash (not `ffmpeg_smoke_fallback`).
