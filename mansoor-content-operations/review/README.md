# Job review shelf

This folder is a review inventory for humans and `print-job-review.py`.
It does **not** change Master Video Editor, Codex workers, or how edits are made.

Codex still works in:

```
/home/box/mansoor-content-operations/jobs/<job-id>/
```

Optional review copies (or pointers) live here:

```
/home/box/mansoor-content-operations/review/<job-id>/
```

A job may have a workspace and no review files yet. That is normal.
`print-job-review.py --job-id <job-id>` prints paths that exist and `MISSING` for the rest. It does not fail on an empty shelf.

## Intended layout per job

```
review/<job-id>/
  final.mp4                 # delivery render (H.264/AAC)
  proxy.mp4                 # review proxy if one was made
  approved-script.txt       # canonical / approved wording
  captions.txt              # burned or sidecar caption text
  cut-manifest.json         # EDL, picture-lock, or cut map
  qc-report.json            # validator / QC output
  meta.json                 # job id, Codex session id, Frame.io ids
```

Filename variants the printer also accepts if they appear under `jobs/<job-id>/` or `review/<job-id>/`:

| Slot | Examples |
| --- | --- |
| final mp4 | `final.mp4`, `*final*.mp4`, `delivery.mp4` |
| proxy mp4 | `*proxy*.mp4` |
| approved script | `*script*`, `canonical*`, `approved-script.txt` |
| caption text | `*caption*` |
| EDL / cut manifest | `*.edl`, `*manifest*`, `picture-lock.json`, `*cut-map*` |
| QC report | `qc-report.json`, `qc-audit.json` |
| ids | `job.json`, `meta.json`, sqlite `jobs.codex_session_id`, Frame.io fields |

Do not put tokens, `.env` files, or Frame.io/Slack/Notion credentials in this folder.

## Skill update shelves (not job media)

- **Current (2026-09-04 real doctrine):** `mansoor-sales-call-skill-update-2026-09-04/` — writable mirror of live `/home/box/.codex/skills/mansoor-sales-call-clips/` plus `NOTES-2026-09-04-real-doctrine-update.md`.
- **Older locked staging (2026-09-03):** `mansoor-sales-call-skill-update/` — owned by `codex-review`; superseded for doctrine content.
