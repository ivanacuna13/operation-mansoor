# MVE Inventory — Live vs Registered vs Installed

Date: 2026-09-08 (PT)  
Host: Eddie Linux box (read-only inventory; no production skill/mve.py edits)  
Canonical live wrapper: `python3 /home/box/mansoor-content-operations/tools/master-video-editor/mve.py`  
Live DB: `/home/box/mansoor-content-operations/state/master-video-editor.sqlite`  
Jobs root: `/home/box/mansoor-content-operations/jobs/`  
Skills root: `/home/box/.codex/skills/`

---

## Executive snapshot

| Route | Live `JOB_REGISTRY` | Skill file exists | Documented in MASTER + dispatch SKILL + MVE profile | Jobs in SQLite | Reaction path wired for its channel |
|---|---|---|---|---|---|
| `sales_call_clip` | yes | yes | yes (2 of 3 docs; TYPE strings drift) | 4 | **partial** — handler only accepts `#sf-video-ready-to-review`; historical assets mapped to `#content-team` |
| `scripted_talking_head` | yes | yes | yes (same drift) | 3 | **partial** (same channel mismatch) |
| `genius_clip` | yes | yes | **no** in MASTER/dispatch/profile (skill-registry yes) | 0 | **partial** / untested; skill text targets `#content-team` |
| `lifestyle_copycat` | yes | yes | **no** in MASTER/dispatch/profile (skill-registry yes) | 0 | **no** — `cmd_reaction` ignores non-`CONTENT_TEAM` channels; lifestyle is `#lifestyle-copycats` |

Biggest factual gaps for project-based editing:
1. Jobs are ad-hoc `workspace/{sources,edit,renders,final,qc,output}` — **no** `00_admin`…`09_archive` layout in live jobs.
2. Editable masters are HyperFrames HTML + JSON manifests / picture-lock JSON / MP4 picture locks — **no** Premiere `.prproj` / AME / Mini SSH bridge code on this box.
3. Docs/profile advertise **2** routes; live registry + skills + skill-registry have **4**.
4. Slack delivery channel drift: live prompt/`system.json` → `#sf-video-ready-to-review` `C0BVAAVASV7`; historical assets + genius skill + profile/dispatch → `#content-team` `C0BQKM27F5F`.

---

## A. Job type registry (critical)

### Live source of truth

`JOB_REGISTRY` in `/home/box/mansoor-content-operations/tools/master-video-editor/mve.py` lines 73–96:

```text
sales_call_clip       → mansoor-sales-call-clips/SKILL.md
                        slack_type: "BOF Sales Call Clips"
                        slack_channel_id: CONTENT_TEAM (= video_delivery_channel_id C0BVAAVASV7)
scripted_talking_head → mansoor-talking-head-scripted-reels/SKILL.md
                        slack_type: "BOF Scripted Talking Heads"
                        slack_channel_id: CONTENT_TEAM
genius_clip           → mansoor-genius-clips/SKILL.md
                        slack_type: "Genius Clip"   # prompt body uses "MOF Genius Clips"
                        slack_channel_id: CONTENT_TEAM
lifestyle_copycat     → mansoor-tof-copycat-editor/SKILL.md
                        slack_type: "Lifestyle Copycat"
                        slack_channel_id: LIFESTYLE_CHANNEL (C0BQTR6RP97)
                        slackbot: copycat-cutter; mention_ivan: False
```

`CONTENT_TEAM` resolves from `config/system.json` → `slack.video_delivery_channel_id` = `C0BVAAVASV7` (`#sf-video-ready-to-review`), **not** human `#content-team`.

There is **no** separate `mve/` Python package beside the wrapper directory; `mve` is a symlink to `mve.py`. Sibling modules: `recovery.py`, `resource_slots.py`, `revision_completeness_gate.py`, `revision_queue.py`, `scheduler.py`, `slack_asset_map.py`.

### Compare surfaces

| Surface | Routes listed | Notes |
|---|---|---|
| Live `mve.py` `JOB_REGISTRY` | 4 | Authoritative for submit/route |
| `/workspace/mve-packets/mve_launch.py` | same 4 keys | **Not byte-identical**: older slack_type labels (`Mansoor Sales Call Clip`, `Scripted Talking Head`); **missing** `delivery-gate` / `revision_completeness` wiring present in live `mve.py` |
| Dispatch SKILL `/home/box/agent-data/workflows/master-video-editor-dispatch/SKILL.md` | **2** only | sales + scripted; channel `#content-team` |
| `MASTER_VIDEO_EDITOR.md` | **2** only | sales + scripted; explicitly “does not … process Lifestyle Copycat” |
| MVE agent profile `…/5d467b50-…/profile.json` | **2** only | sales + scripted; Slack review in `#content-team` |
| `config/skill-registry.json` | all 4 (+ playbook-less formats) | Maps Notion formats → editor skills including Genius + TOFU Copycat |

### Per-route detail

#### 1) `sales_call_clip`
- **Registered in live mve.py?** yes  
- **Skill path:** `/home/box/.codex/skills/mansoor-sales-call-clips/SKILL.md` — **exists** (also `agents/`, `references/`, `scripts/qc_sales_call.py`)  
- **Documented MASTER / dispatch?** yes (both list it)  
- **Jobs used (sample):**  
  - `sales-call-june-consulting-20260630` (AWAITING_REVIEW, rev 0)  
  - `import:sales-call-04-felony:v1` (Edit Revisions Needed, rev 4)  
  - `import:sales-call-05-twenty:v1` (AWAITING_REVIEW, rev 1)  
  - `import:sales-call-06-policy:v1` (Edit Revisions Needed, rev 5)  
- **Revision/reaction path?** yes in principle: `memo` → `cmd_reaction` → `cmd_review` → resume Codex with `notes_resume_prompt` + Frame checklist + `delivery-gate`. **Channel gate:** reactions ignored unless `channel_id == CONTENT_TEAM` (`C0BVAAVASV7`). All six DB assets currently store `slack_channel_id=C0BQKM27F5F` (`#content-team`).  
- **Slack delivery + bot:** Prompt requires MVP Agency **`copycat-cutter`**, never Ivan; channel `#sf-video-ready-to-review` `C0BVAAVASV7`; TYPE `BOF Sales Call Clips`; mention Ivan; Headline + FILE (Frame public link). Skill reference still says TYPE `Mansoor Sales Call Clip` in places — label drift vs live prompt/`system.json`.

#### 2) `scripted_talking_head`
- **Registered?** yes  
- **Skill:** `/home/box/.codex/skills/mansoor-talking-head-scripted-reels/SKILL.md` — exists (`scripts/validate_reel.py`, `build_boundary_audit.py`, `measure_speech_gaps.py`, references)  
- **Documented MASTER / dispatch?** yes  
- **Jobs:** `import:recognition:v1` (rev 7), `import:lone-wolf:v1` (rev 3), `import:recruiting-cycle:v1` (rev 4)  
- **Revision/reaction?** same shared path as sales; same channel mismatch risk  
- **Slack:** `copycat-cutter`, `#sf-video-ready-to-review`, TYPE `BOF Scripted Talking Heads`, Ivan mention, Headline + FILE

#### 3) `genius_clip`
- **Registered?** yes  
- **Skill:** `/home/box/.codex/skills/mansoor-genius-clips/SKILL.md` — exists (skill only; doctrine under `/home/box/mansoor-content-operations/context/genius/`)  
- **Documented MASTER / dispatch / profile?** **no**  
- **Jobs in live SQLite?** **none**  
- **Revision/reaction?** skill text says resume original Codex + Frame stack; dispatcher would route memo via shared path **if** delivered to `CONTENT_TEAM`. Skill itself tells worker to Slack `#content-team` `C0BQKM27F5F` with TYPE `Genius Clip` — **conflicts** with live `mve.py` prompt (`#sf-video-ready-to-review`, TYPE `MOF Genius Clips`) and with `cmd_reaction` channel filter.  
- **Bot:** skill says `copycat-cutter`; never as Ivan

#### 4) `lifestyle_copycat`
- **Registered?** yes  
- **Skill:** `/home/box/.codex/skills/mansoor-tof-copycat-editor/SKILL.md` — exists (doctrine under `context/copycat/`)  
- **Documented MASTER / dispatch / profile?** **no** (MASTER says MVE does not process Lifestyle Copycat; Eddie owns emoji loop)  
- **Jobs in live SQLite?** **none**  
- **Revision/reaction?** skill uses ✍️ `writing_hand` (not 📝) in `#lifestyle-copycats`; Eddie automation. Live `mve.py` `REACTION_MAP` only has white_check_mark / heavy_check_mark / memo / x — **no** `writing_hand` / star-struck. `cmd_reaction` **ignores** non-`CONTENT_TEAM` channels → lifestyle reactions are **not** wired through MVE reaction handler.  
- **Slack:** `copycat-cutter` only to `#lifestyle-copycats` `C0BQTR6RP97`; TYPE `TOF Copy Cats` / skill `Lifestyle Copycat`; **never** mention Ivan; Drive FILE link (not Frame) per skill; Ready-to-Post 3-file pack on ✅/🤩

---

## B. Skill paths — approach summary

### `mansoor-sales-call-clips`
- **Editable project vs MP4-only revision:** HyperFrames composition (`index.html` / `hyperframes.json`) + `sales-call-spec.json` + speaker-aware `edit-map` / picture-lock media. Revisions are Frame-comment driven re-cuts of the composition — **not** “edit the previous review MP4 as source,” but picture-lock MP4s are intermediate artifacts that revisions often regenerate from. No Premiere project.  
- **Folder layout (skill):** project-local workspace; observed jobs use ad-hoc `workspace/{assets,final,qc,output,snapshots,.media}` — not `00_admin`…`09_archive`.  
- **QC gates:** `scripts/qc_sales_call.py` + manual contact-sheet / crop / bleep / join inspection; CFR H.264 prep (`-g 30`) before HyperFrames; Frame transcode + public HTTP 200.  
- **Frame.io:** via `frameio-review-loop` skill + `/home/box/mansoor-content-operations/tools/voiceedit/`; upload into existing stack on revise.  
- **Render:** HyperFrames (+ ffmpeg prep).  
- **Model:** not set inside skill; worker launched by MVE as `gpt-5.6-sol` / reasoning `high`.

### `mansoor-talking-head-scripted-reels`
- **Editable project:** `picture-lock.json` (source-linked segments) + HyperFrames `index.html` / captions; revisions regenerate picture lock from original camera + external mic — doctrine forbids treating checker/upload as pass. Observed jobs keep `sources/*.MP4`, `edit/*Picture-Lock*.mp4`, `renders/*Final*.mp4`.  
- **Folder layout:** ad-hoc `workspace/{sources,edit,renders,qc,transcripts,scripts,output,snapshots}` — not numbered bins.  
- **QC:** boundary audit strips (`build_boundary_audit.py`), `measure_speech_gaps.py` (−32 dB), `validate_reel.py` (self-attested audit JSON + probe + full decode).  
- **Frame.io:** stack upload; newest transcoded head required.  
- **Render:** HyperFrames / ffmpeg picture-lock then styled final.  
- **Model:** via MVE (`gpt-5.6-sol`).

### `mansoor-genius-clips`
- **Editable project:** Premiere-style **process** described (waveform razor, face fill) but Linux skill is ffmpeg/manual cut + doctrine files — **no** `.prproj` on box. MP4 export is the deliverable; revisions = recut from long source, not from prior review MP4 as camera substitute.  
- **Folder:** not standardized under MVE jobs (0 jobs). Context doctrine under `context/genius/`.  
- **QC:** DEFINITION-OF-DONE + full-speed watch; Frame via voiceedit tools.  
- **Frame.io:** yes (skill).  
- **Render:** ffmpeg H.264 1080×1920 (explicit export settings). HyperFrames not required.  
- **Model:** MVE launch model; skill does not name Astra.

### `mansoor-tof-copycat-editor`
- **Editable project:** clip list / cut notes under `/workspace/copycats/`; helper `cut_tof10_v01.py`; remakes from B-roll library — not HyperFrames talking-head stack. Revisions from Drive comments (✍️), filename ` v2`.  
- **Folder:** `/workspace/copycats/{md,audio,cuts,out}` + Drive Ready-to-Post day folders — not MVE `jobs/` numbered layout.  
- **QC:** QUALITY.md + freezedetect + listen/read hooks.  
- **Frame.io:** **not** primary; Drive upload.  
- **Render:** ffmpeg concat/burn (copycat helpers).  
- **Model:** MVE if routed; skill does not name Astra.

---

## C. Job workspace layout (sampled)

**Pattern:** every sampled MVE job is `jobs/<job_id>/workspace/…` (or flat job dir for june consulting). **Zero** `00_admin` / `01_originals` / `04_projects` / `07_exports` directories found under `jobs/`.

### Sales call — `import:sales-call-04-felony:v1`
```text
import:sales-call-04-felony:v1/
  workspace/
    BRIEF.md, AGENTS.md, sales-call-spec.json, edit-map.json, transcript.json
    hyperframes.json, index.html, package.json, meta.json
    assets/          picture-lock*.mp4, dialogue*, name-bleep*
    final/           Mansoor-Sales-Call-04-…-v4.mp4, …-v5.mp4
    qc/              ffprobe*, loudness*, sha256*, contact sheets, frame-comment-checklist*.json, delivery-gate.json, revision-v5/, …
    output/          frameio_review.json, worker-result.json, slack-revision-reply.json, mve-delivery-gate.sqlite, …
    snapshots/       frame-*.png, contact-sheet-*.jpg
    .media/          manifest.jsonl, audio/, video/, images/
```
Ad-hoc: `workspace/renders` not used here; uses `assets` + `final` + `qc` + `output`.

### Scripted — `import:lone-wolf:v1`
```text
import:lone-wolf:v1/
  workspace/
    sources/         Mansoor - The Lone Wolf - Raw.MP4
    edit/            Picture-Lock-v3.mp4 + revision3-*.json + build scripts
    renders/         Final-v2.mp4, Final v3.mp4
    qc/              frame-comment-checklist.REQUIRED.json, revision3/
    transcripts/, final_transcripts/, scripts/, music-originals/
    assets/, output/, snapshots/, revision2-snapshots/
    picture-lock.json, captions.json, index.html, hyperframes.json
    MAC_PATHS.txt    (legacy Mac HyperFrames paths — not Mini Premiere bridge)
```

### Sales — `sales-call-june-consulting-20260630` (alternate flat layout)
Top-level (no nested `workspace/` only): `audio/`, `candidates/`, `qc/`, `scripts/`, `transcripts/`, `disposable/`, plus codex logs — still ad-hoc, not `00_admin`…`09_archive`.

---

## D. State / SQLite

### Master Video Editor ledger
Path: `/home/box/mansoor-content-operations/state/master-video-editor.sqlite`  
Override env: `MVE_DB`

| Table | Rows (2026-09-08) | Role |
|---|---|---|
| `jobs` | 7 | job_id, job_type, assignment_hash, codex_session_id, vm_*, selected_skill, packet, status, produced_assets, frameio_links, slack_message_ids, asset_review_state, revision_count, workspace, legacy_mac_session_ids, pipeline, notion_url, … |
| `assets` | 6 | per-deliverable Slack ts / Frame asset / status / revision_running |
| `asset_slack_messages` | 17 | slack_message_ts ↔ asset_id/job_id/channel/kind (delivery vs revision_reply) |
| `reaction_events` | 45 | idempotent reaction log (1 approved, 44 notes) |
| `audit_log` | 115 | append-only dispatcher actions |

### Content PM
Path: `/home/box/mansoor-content-operations/state/content-pm.sqlite`  
Tables: `objects`, `deliveries` (slack_channel_id, root_ts, frame_url, delivery_state), `events`, `intents`, `pending_notion`, `transitions`, `shoot_batches` (0), `jobs` (0 rows — PM job table unused vs MVE jobs).

Other state nearby (not MVE core): `drive-sweeper.sqlite`, `idea-guy.sqlite`, `notifications.sqlite`, `mve-scheduler/`.

### Sessions
Codex session IDs stored on `jobs.codex_session_id`; early persist from JSONL `thread.started`. Rollouts under `~/.codex/sessions/`. Legacy Mac session IDs retained in `legacy_mac_session_ids` / `legacy_session_status` for import jobs that cannot resume Mac threads.

---

## E. QC & revision identity gaps

### What is already fail-closed (good)
- `revision_completeness_gate.py`: requires `qc/frame-comment-checklist.json` with every `fixed=yes` and `unresolved_frame_comments_remaining==0` before Slack / Edit Ready for Review.  
- Live sample `import:sales-call-04-felony:v1`: live Frame comment fetch **failed** (DNS); checklist correctly blocked delivery (`may_post_slack: false`).  
- `validate_reel.py`: `--no-full-decode` **adds an error** (cannot approve); measured gap limits enforced.  
- Config flags: `REQUIRE_FRAME_COMMENT_CHECKLIST: true`, `FAILCLOSED_REVISION_DELIVERY_GATE: true`.

### Concrete false-pass / identity risks

1. **Self-attested audit booleans** — `validate_reel.py` ~L227–311: many fields (`direct_eye_contact`, `quiet_word_tails_checked`, `full_resolution_reviewed`, visual/audio batch flags, etc.) pass if JSON says `true`. An editor (or model) can set `true` without independent measurement. Spec §7 asks to remove automatically asserted listening/word-integrity/visual-pass flags — this is the main residual pattern.  
2. **Process success ≠ media/upload/approval** — dispatcher can record Codex exit / worker JSON while Frame fetch fails; sales04 shows blocked gate, but Notion/Slack state can still drift if workers bypass `mve.py delivery-gate`.  
3. **Frame.io stack head** — `tools/voiceedit/frameio_review.py` ~L526–672 verifies `expected_head_id`, `expected_head_name`, `head_transcoded` after upload into `version_stacks`. Gap: **pre-comment-read** “resolve latest stack head” is instructed in prompts/skills but not a hard shared library call enforced before every revision start; depends on worker discipline.  
4. **Slack channel / reaction identity** — `mve.py` `cmd_reaction` L1429–1431: `if channel and channel != CONTENT_TEAM: ignored`. Historical assets on `C0BQKM27F5F` vs `CONTENT_TEAM=C0BVAAVASV7` → reactions on the channel where reviews actually live may be ignored by live code. Lifestyle channel never accepted.  
5. **TYPE / channel label drift** across `JOB_REGISTRY.slack_type`, worker prompt blocks, skill SKILL.md, and `system.json.video_delivery_format` (e.g. Genius: `Genius Clip` vs `MOF Genius Clips`; sales: `BOF Sales Call Clips` vs skill `Mansoor Sales Call Clip`).  
6. **MP4-as-timeline risk** — jobs store successive `picture-lock-vN.mp4` / `final/*-vN.mp4` without immutable original↔timeline map contract; revisions can be tempted to recut from prior export (especially sales HyperFrames path). Spec wants versioned source timeline + hashes.

No literal `qc_passed = True` defaults found in the two primary validators; risk is **attestation** and **channel/state confusion**, not a hardcoded always-pass constant.

---

## F. Premiere / Mac Mini

**No live Premiere/AME/SSH Mini bridge implementation on this box.**

Findings:
- No `.prproj` under `/home/box/mansoor-content-operations/jobs` or `/workspace` (except design doc).  
- No Media Encoder queue worker / Premiere scripting bridge package in `tools/master-video-editor/`.  
- `MAC_PATHS.txt` in lone-wolf points at **legacy Mac HyperFrames** paths under `/Users/ivanacuna/Documents/Codex/...`, not Mini Premiere.  
- Design-only doc already drafted: `/workspace/EDDIE BRAIN/MVE_PROJECT_SYSTEM/06_PREMIERE_BRIDGE.md` (orchestration contract; Mini paused).  
- Genius skill *describes* Premiere sit-down face-fill and waveform razor as editorial doctrine; that is process language, not installed Mini automation.  
- Do **not** SSH to Mini for this inventory (per task).

---

## G. Astra / model

| Item | Value |
|---|---|
| Canonical model | `gpt-5.6-sol` from `config/system.json` → `codex.model` (`REQUIRED_MODEL` in mve.py L55) |
| Reasoning | `high` (`REQUIRED_REASONING`) |
| Host | `cursor` |
| Availability check | `~/.codex/models_cache.json` must contain `gpt-5.6-sol` (`model_available()`); cache present and contains sol |
| Observed mismatch | If JSONL reports another model → fail closed `BLOCKED: REQUIRED CODEX MODEL UNAVAILABLE` (mve.py ~L796–801) |
| “Astra” string | **Not** present as a separate model id in `system.json` / MVE config; operational synonym in the project brief for the locked Codex sol model |
| Silent downgrade path | **Code exists:** `launch_codex()` → `tools/content-os/worker_launch.py` can launch **`grok-4.6` / `xhigh`** when forced or when Codex fails and fallback enabled. Live `master-video-editor.json` sets `FALLBACK_WORKER_ENABLED: false`, `USE_GROK_FALLBACK_FIRST: false`, `PRIMARY_WORKER: codex` — **currently disabled**. Caveat: if config load fails (`cfg={}`), `fallback_enabled({})` returns **True** (because `None is not False`). |
| Skill fallback | `NEVER_FALLBACK_EDIT_SKILL=general-video` — skill_for refuses general-video substitution |

Docs/profile correctly forbid Grok/other model/lower reasoning for editorial work; code path for Grok fallback is the residual silent-substitution risk if flags flip or config fails.

---

## Delivery / bot identity (cross-cutting)

- Outbound Slackbot: Composio **`copycat-cutter`** (`system.json` `slack.slackbot_connection` / `outbound_connection`).  
- Never post as Ivan (`U0BQJP0DEGH`); `never_post_as` + `fail_closed_identity`.  
- Authorized reviewers: Ivan + Daud + Agung (`authorized_reviewer_ids`).  
- Video channel (live MVE): `#sf-video-ready-to-review` `C0BVAAVASV7`.  
- Lifestyle: `#lifestyle-copycats` `C0BQTR6RP97`.  
- Ready-to-post: Drive day folders; Slack ready-to-post channel noted OFF for auto-post in `video_approve_delivery`.

---

## Registered vs live gap (summary table)

| Claimed somewhere | Live dispatcher |
|---|---|
| Docs/profile: 2 job types | Registry: 4 |
| Docs: review in `#content-team` | Code: reactions only on `C0BVAAVASV7`; assets historically `C0BQKM27F5F` |
| Genius skill: Slack `#content-team` + TYPE Genius Clip | mve prompt: `#sf-video-ready-to-review` + MOF Genius Clips |
| MASTER: MVE does not process Lifestyle Copycat | Registry includes `lifestyle_copycat` |
| Spec desire: Premiere native masters | Box reality: HyperFrames/ffmpeg only; Mini bridge absent |
| Spec desire: `00_admin`…`09_archive` | Live jobs: ad-hoc workspace trees |
| Model: Astra / no silent downgrade | Locked `gpt-5.6-sol`; Grok fallback code present but disabled |

---

## Recommended next implementation order (inventory conclusion)

1. **Freeze identity contracts** — single channel map + TYPE labels + reaction allowlist (include lifestyle channel or explicitly keep Eddie-owned loop); align dispatch SKILL + MASTER + profile to live 4-type registry without changing approved edits.  
2. **Project/version contract** — immutable originals, picture-lock/manifest as editable master, ban review-MP4-as-source; introduce `00_admin`…`09_archive` for **new** jobs only.  
3. **QC attestation repair** — replace self-attested visual/listening flags with measured evidence where possible; keep delivery-gate.  
4. **Batch / single-writer ownership** — one analysis per source; per-deliverable QC/upload.  
5. **Premiere/Mini bridge** — only after box contracts exist; currently blocked (no install/automation on Mini in this inventory).  
6. **Pilot** — one scripted batch + multi-clip sales call using new layout; genius/copycat after channel/docs fixed.

