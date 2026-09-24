# Changes — 2026-09-08 (PT) MVE project-system slice

## Pass A (earlier) — foundation
Pass goals: align docs to live 4-type registry; freeze reaction channel allowlist; add shared layout + revision identity helpers for **new** jobs; update MVE_PROJECT_SYSTEM docs. No Mini SSH, no Codex media launches, no approved-edit rewrites, no destructive media migration.

### Files changed (Pass A)
- Docs/profile: `MASTER_VIDEO_EDITOR.md`, dispatch SKILL, MVE profile description
- `mve.py` reaction allowlist + `init-layout`; `project_layout.py`; `revision_identity.py`; `AGENTS_PROJECT_RULES.md`
- `07_SLACK_IDENTITY.md`, this file, PROGRESS/TODO

## Pass B (this pass) — QC / Frame head / success_layers / batch stub
Constraints unchanged: box only; no Mini SSH; no Codex media launches; no approved-edit rewrites; lifestyle review Eddie-owned.

### Code
- **New** `tools/master-video-editor/frameio_stack_head.py` — `resolve_stack_head()` reusing voiceedit Frame OAuth/API; fail closed; callers must resolve before comment read and before upload
- `revision_completeness_gate.py` — require distinct `success_layers` (`process_ok`, `media_ready`, `upload_complete`, `playback_ready`, `delivery_complete`, `approved`); missing layers ⇒ incomplete; evidence paths/hashes required for media/upload/playback/delivery claims; worker must never set `approved`
- `mve.py` — notes/revision + worker prompts mention stack-head helper + success_layers; `FALLBACK_WORKER` fail-closed if config/key missing; persist `worker-model.json` + audit model/reasoning/effort
- `tools/content-os/worker_launch.py` — `fallback_enabled` requires explicit `FALLBACK_WORKER_ENABLED is True` (missing ⇒ disabled)
- **New** `batch_ownership.py` — `analysis_cache_key` + advisory `assert_single_native_writer` under `04_projects/` (no Premiere)
- Talking-head `validate_reel.py` — listening/word-integrity/visual self-attestations quarantined as `attestation_only` / excluded from pass aggregation (measurements not clamped)
- Sales `qc_sales_call.py` — optional `--audit`; known self-attested keys quarantined; cannot alone set `ok`
- Four format `SKILL.md` files — small **Shared project rules** pointer to `AGENTS_PROJECT_RULES.md` (never review-MP4-as-source; success_layers; Frame head)

### Tests / verify
- `tests/master-video-editor/test_success_layers_gate.py` — fail-closed on missing layers / collapsed ok / worker-approved / missing evidence
- `py_compile` on touched Python modules
- No Codex launched this pass

### Backups
- `mve.py.bak-success-layers-*`
- `revision_completeness_gate.py.bak-*`
- `validate_reel.py.bak-*` / `qc_sales_call.py.bak-*`
- `worker_launch.py.bak-*`

## Pass C (this pass) — wire revision_identity into live write path
Constraints unchanged: box only; no Mini SSH; no Codex media launches; no approved-edit rewrites; no legacy media migration.

### Code
- **Extended** `revision_identity.py` — `ensure_identity_tree`, `record_revision_attempt`, `mark_revision_approved`, `identity_status`, `build_revision_record`, worker-model/result binders; writes `00_admin/pointers.json` + `00_admin/revisions/<id>.json` (mirror under `04_projects/revisions/`); `approved` never set from worker path
- `mve.py` — after `_run_job` gate-block / completion: `_safe_record_revision_identity`; `cmd_delivery_gate` records attempt; `cmd_review` ✅ → `_safe_mark_approved_identity` (pointer + status_layer approved + delivery_history); rejected records checkpoint/rejected; `cmd_reaction` forwards `reacting_user_id`; CLI `identity-status --job-id` (read-only)
- Legacy jobs: `ensure_batch_tree` on job root **without moving media** when numbered tree missing

### Tests / verify
- `tests/master-video-editor/test_revision_identity_write.py` — synthetic worker-result → identity files; approved reaction updates pointer; missing tree created empty; worker cannot flip approved
- `py_compile` on `revision_identity.py` / `mve.py`; prior success_layers + reaction channel tests still pass
- Dry identity-only exercise (temp dir) succeeded — pilot unblocked for identity-only dry run (no Codex/Frame)

### Backups
- `mve.py.bak-identity-*`
- `revision_identity.py.bak-*`

## Intentionally not changed
- Existing job media trees (no moves)
- Lifestyle reaction automation (Eddie)
- Approved published edits / Premiere Mini bridge
- Live `JOB_REGISTRY` skill paths
