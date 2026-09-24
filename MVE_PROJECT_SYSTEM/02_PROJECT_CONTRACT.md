# Shared project-based editing contract

Status: DRAFT — implement across all registered MVE job types.
Host: Eddie Linux VM orchestration. Native Premiere master lives on Mini when used; Linux keeps manifests/XML/hashes/state.

## Non-negotiables
1. Revisions edit the **versioned editable project** (manifest + timeline + linked sources), never a prior review MP4 as if it were camera source.
2. Originals are **immutable**. Proxies/analysis/renders/captions/graphics/caches are separate layers.
3. Every deliverable keeps a **source→timeline mapping** (source IDs, frame indexes, timecode when present, sample/time audio positions).
4. One **revision_id** binds: manifest, interchange XML (if any), native project checkpoint (if any), export hash, QC evidence, Frame.io asset/stack head.
5. If recovery of originals or mapping fails → precise **BLOCKED**, no destructive guess-repair.
6. Finished reference MP4 may be reference/insert only — not a substitute for missing edit sources.
7. XML is interchange, not a lossless Premiere substitute. Native-only features stay in `.prproj`; do not regenerate simplified XML over a finished native edit.

## Identity objects

### media_asset
- `media_id` (stable)
- `path` or controlled reference to shared originals store
- `sha256`, bytes, duration, fps/timebase, channel map, timecode start (if any)
- `role`: original | proxy | analysis_audio | render | caption | graphic | music | sfx | cache

### timeline_map (per deliverable sequence)
- `deliverable_id`, `sequence_id`, `revision_id`
- clips: `{clip_id, media_id, src_in_frame, src_out_frame, tl_in_frame, tl_out_frame, audio_in_sample?, audio_out_sample?, handles, effects_ref?}`
- parent_revision_id, change_list[]

### revision_record
- `revision_id`, `parent_revision_id`
- `project_revision` (native or manifest version)
- `editor_model`, `effort`, timestamp
- `source_hashes[]`, `asset_hashes[]`
- `export_sha256?`, `qc_evidence_path?`
- `frameio_asset_id?`, `frameio_stack_id?`, `stack_head_verified_at?`
- `status_layer`: working | checkpoint | delivered | approved | rejected

## Layer classification for revisions
`source_timing` | `captions` | `graphics` | `sound` | `delivery`
Run affected checks + proportionate regression. Graphics-only must preserve approved source ranges/audio. Upload retry must not re-render.

## Pointers (append-only history + explicit heads)
- `current_working_revision`
- `current_approved_revision` (null until approved)
- `delivery_history[]` append-only
Never overwrite delivered/approved milestones. Working copy may update in place only for non-milestone saves.

## Output promotion
Write temp → verify complete → promote. Delivery retry ≠ new editorial revision ≠ duplicate upload.

## Format doctrine stays in skills
This contract does not replace sales/scripted/genius/copycat editorial rules. It only mandates project/version/QC identity.
