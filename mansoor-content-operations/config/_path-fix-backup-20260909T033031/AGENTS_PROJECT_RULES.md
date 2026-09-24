# MVE shared project rules (skills pointer)

Skills and editor Codex sessions should treat this as shared doctrine across all registered job types (`sales_call_clip`, `scripted_talking_head`, `genius_clip`, `lifestyle_copycat`). Format-specific editorial rules stay in each skill.

## Hard bans
1. **Never treat a review / export MP4 as camera source.** Revisions edit the versioned editable project (manifest / picture-lock / timeline + linked originals), not the previous review movie as if it were the recording.
2. **Originals are immutable.** Do not overwrite files under `01_originals/` or original camera/audio paths. Proxies, analysis, renders, captions, graphics, and caches live in their own bins.
3. **Do not migrate approved media trees destructively.** Numbered layout is for new work; legacy `workspace/` trees stay put unless a separate retention decision authorizes a non-destructive migrate.

## Success layers (distinct booleans)
Never collapse into a single `qc_passed` / `ok`. Record separately:
- `process_ok`
- `media_ready`
- `upload_complete`
- `playback_ready`
- `delivery_complete`
- `approved`

A clean process exit, valid XML, successful decode, or upload is **not** proof of clean cuts or approval.

## Frame.io stack head
Resolve the **actual latest stack head** before reading comments and again before upload. Bind the job to asset ID, comment IDs, sequence/project revision, and render hash. Detect newer heads mid-job.

Helper: `python3 /home/box/mansoor-content-operations/tools/master-video-editor/frameio_stack_head.py <asset_or_stack_id>`
(reuses `/home/box/mansoor-content-operations/tools/voiceedit/frameio_review.py` OAuth/API; fail closed).

## Revision identity
Write / update `00_admin/pointers.json` (`current_working_revision`, `current_approved_revision`, append-only `delivery_history`). Persist `revision_record` JSON validated against `schemas/revision_record.schema.json` (local tools copy).

## Layout
Prefer `00_admin`…`09_archive` under `jobs/<job_id>/` (alongside legacy `workspace/`). See `project_layout.py` and `03_FOLDER_LAYOUT.md`.

## Lifestyle exception
Lifestyle Copycat delivery is `#lifestyle-copycats`. Its review loop is Eddie's emoji automation — **not** the MVE memo/reaction map on `#sf-video-ready-to-review`.
