# QC and revision identity contract

## Forbidden
- Auto-asserted listening / word-integrity / visual-pass flags without measured evidence
- Clamping measurements to passing limits
- Treating valid XML / successful decode / process exit / upload as proof of clean cuts
- Approving solely by rereading the editor's pass flags
- Promoting a blocked worker to Edit Ready for Review because it returned text

## Untouched ASR vs editorial text
Keep separate. Never overwrite ASR with corrected captions in the analysis store.

## Pre-first-review gate (required order)
1. Lightweight source-linked cut
2. Inspect joins, pauses, clipped phonemes, eye contact, discontinuities
3. Replace bad takes / adjust ranges
4. Lock picture timing → then captions
5. Inspect finished export; evidence against **export hash**

## Frame.io binding
Before comment read AND before upload: resolve **actual stack head**.
Bind job to: asset_id, comment_ids, sequence_id, project_revision, render_hash.
Detect newer head mid-job, ownership conflicts, duplicate filenames.
Map review timestamps through the reviewed revision → original sources.
One stable review stack/link per deliverable; preserve old comments.

## Success layers (distinct booleans)
`process_ok` | `media_ready` | `upload_complete` | `playback_ready` | `delivery_complete` | `approved`
Do not collapse these into a single `qc_passed` or `ok`.
