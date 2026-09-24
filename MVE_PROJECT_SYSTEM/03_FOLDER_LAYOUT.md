# Batch / recording folder layout

Adapt under existing job roots:
`/home/box/mansoor-content-operations/jobs/{{job_or_batch_id}}/`

Legacy jobs often use `workspace/{renders,final,qc,output}`. New work and migrations use:

```text
BATCH_OR_RECORDING_ID/
  00_admin/     brief, source inventory, deliverable roster, pointers.json
  01_originals/ immutable media or refs to shared originals store
  02_proxies/   rebuildable proxies + analysis audio
  03_analysis/  untouched ASR, candidates, source notes (cache by media hash + model/settings)
  04_projects/  versioned manifests, XML, native project checkpoints
  05_assets/    versioned captions, graphics, music, SFX (never silently overwrite shared PNGs)
  06_qc/        evidence tied to exact revision_id + export sha256
  07_exports/   versioned masters + review files (temp then promote)
  08_delivery/  Frame.io IDs, comments, upload/playback receipts
  09_archive/   archival manifests + restore instructions
```

## Naming
```text
MAN_BATCH_YYYYMMDD_<slug>_project_rNNN.prproj
MAN_<SOURCE>_<DELIV>_edit_rNNN.json
MAN_<SOURCE>_<DELIV>_9x16_review_rNNN.mp4
```
Separate: project revision vs per-deliverable revision vs export preset variant. Stable IDs over titles. Approval is metadata on exact asset/revision — do not rename to FINAL as the approval mechanism.

## Bins / sequences
- Source recordings bin
- Selects / stringout (discovery only)
- One export sequence per independently reviewed deliverable

## Checkpoints
Before material change: immutable project checkpoint. Autosave ≠ backup. Independent backup of originals + milestones; restore/relink test required before treating backup as real.
