# MVE Project / Version / Batch System — Progress

Home: `/workspace/EDDIE BRAIN/MVE_PROJECT_SYSTEM/`  
Source spec: `SOURCE_SPEC.md`  
Machine: Eddie's Linux VM (not Mini), unless a step explicitly needs Premiere/AME SSH submit later.  
Inventory: `01_INVENTORY.md` (complete 2026-09-08 PT)

Last updated: 2026-09-08 ~13:34 WEST (Premiere download on Mini)

## Status legend
- [ ] not started
- [~] in progress
- [x] done
- [!] blocked

## Sections (from SOURCE_SPEC)

### 1. Inventory live MVE routes
- [x] Deep inventory written → `01_INVENTORY.md`
- Confirmed live `JOB_REGISTRY` = 4 types; skills exist; ad-hoc workspaces; no Premiere on box; channel mismatch documented

### 2. Project-based editing foundation
- [x] Contracts drafted: `02_PROJECT_CONTRACT.md`
- [x] `revision_identity.py` + schema copy under tools (pointers + revision_record validate)
- [x] `AGENTS_PROJECT_RULES.md` (ban review-MP4-as-source; immutable originals; success_layers; Frame head)
- [x] Helpers pointed from format skills; live revision write path consumes `revision_identity` (pointers + revision_record on gate/complete/approve)
- [ ] Premiere XML vs native master enforcement (later / Mini)

### 3. Folder structure + naming + immutable milestones
- [x] Contract: `03_FOLDER_LAYOUT.md`
- [x] `project_layout.py` `ensure_batch_tree` / `map_legacy_workspace` (no moves)
- [x] New submits / `mve.py init-layout --job-id` create `00_admin`…`09_archive` under `jobs/<id>/`
- [x] Append-only `delivery_history` + working/approved pointers on live revision path (version naming still lightweight)

### 4. Astra editorial / Grok queue ownership
- [x] Inventory: editorial = Codex `gpt-5.6-sol`; Grok = dispatch/state only
- [x] Harden empty-cfg Grok fallback fail-closed (`FALLBACK_WORKER_ENABLED` must be explicit True)
- [x] Log model/effort on launch → `worker-model.json` + `codex_result` audit fields
- **Astra lock (proven 2026-09-08):** editorial = `gpt-6-astra` / reasoning `medium`. Dry worker session observed both values in Codex rollout. Fail closed: `BLOCKED: GPT-6-ASTRA MEDIUM UNAVAILABLE`.

### 5. Batch related work / isolate deliverables
- [x] Scaffold: `04_BATCH_CONTRACT.md`
- [x] Stub code: `batch_ownership.py` (`analysis_cache_key`, advisory single-writer lock under `04_projects/`)
- [ ] Premiere native writer integration (Mini)

### 6. Premiere / AME integration
- [x] Inventory: none on box; design-only `06_PREMIERE_BRIDGE.md`
- [x] Mini Premiere Pro 2026 **26.3.2** + Media Encoder 2026 **26.3.2** + Photoshop 2026 **27.10.0** installed (verified). Bridge operational work in progress.

### 7. QC + revision identity repair
- [x] Fail-closed Frame checklist + delivery-gate live; **success_layers** now required (missing ⇒ incomplete)
- [x] Slack reaction channel allowlist frozen (`07_SLACK_IDENTITY.md`)
- [x] Kill/quarantine self-attested visual/listening pass flags (talking-head + sales QC)
- [x] Shared Frame stack-head resolve helper (`frameio_stack_head.py`); wired into mve prompts
- [x] Distinct success_layers in delivery-gate
- [ ] Live pilot proving workers emit success_layers + evidence

### 8. Connect formats + pilot verify
- [x] Align MASTER + dispatch SKILL + MVE profile description to live **4**-type registry + correct Slack channels
- [x] Connect shared contracts into all format skills (Shared project rules pointer)
- [x] Synthetic dry pilot measured (`09_PILOT_STATUS.md`)
- [ ] Live Codex+Frame pilot on new assigned job

## Decisions locked
- Implementation host = Eddie box, not Mini
- Do not rewrite approved published edits / publish replacements
- Do not migrate existing job media trees destructively
- Lifestyle review stays on Eddie / `#lifestyle-copycats` — not MVE memo map
- Live video Slack SoT = `#sf-video-ready-to-review` `C0BVAAVASV7`
- Editorial model = `gpt-6-astra` / medium (fail-closed); Grok fallback disabled unless `FALLBACK_WORKER_ENABLED: true`
