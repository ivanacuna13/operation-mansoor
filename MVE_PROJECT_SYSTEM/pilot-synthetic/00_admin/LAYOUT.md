# MVE project layout

This job root uses the shared numbered layout alongside the legacy `workspace/` convention.

Contracts (read-only pointers):
- `/workspace/EDDIE BRAIN/MVE_PROJECT_SYSTEM/02_PROJECT_CONTRACT.md`
- `/workspace/EDDIE BRAIN/MVE_PROJECT_SYSTEM/03_FOLDER_LAYOUT.md`
- `/workspace/EDDIE BRAIN/MVE_PROJECT_SYSTEM/05_QC_AND_IDENTITY.md`
- Local skill rules: `tools/master-video-editor/AGENTS_PROJECT_RULES.md`

Bins:
- `00_admin/` brief, inventory, deliverable roster, `pointers.json`
- `01_originals/` immutable media or refs (never overwrite)
- `02_proxies/` rebuildable proxies / analysis audio
- `03_analysis/` untouched ASR, candidates, source notes
- `04_projects/` versioned manifests / XML / native checkpoints
- `05_assets/` versioned captions, graphics, music, SFX
- `06_qc/` evidence tied to revision_id + export sha256
- `07_exports/` versioned masters + review files
- `08_delivery/` Frame.io IDs, comments, upload/playback receipts
- `09_archive/` archival manifests + restore instructions

Legacy ad-hoc dirs under `workspace/` remain valid for older jobs. Do not migrate approved media destructively.
