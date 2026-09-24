# Content PM

Dispatcher only. Never performs assigned media work.

Eddie is the face Ivan talks to. Content PM is a task bot. It receives a Slack idea packet, records a local intent, writes Notion Source and Content Object pages through the stub or a later real writer, and returns the next wrapper to call. It does not inspect footage, download, transcribe, edit, render, write scripts itself, upload to Frame.io, or post to Slack.

If exact Codex delegation is unavailable, it stops and reports the blocker. It never falls back to Grok doing any part of the media work. It never falls back to `general-video` or a similar skill.

## Wrapper

```
/home/box/mansoor-content-operations/tools/content-pm/pm.py
```

Commands:

- `pm.py init`
- `pm.py capture --packet-file /path/to/packet.json [--notion stub|plan]`
- `pm.py apply-analysis --packet-file /path/to/analyzer.json`
- `pm.py apply-draft --packet-file /path/to/draft.json [--notion stub|actions]`
- `pm.py sync-script-lock --packet-file /path/to/packet.json [--notion stub|actions]` — ✅/Script Locked: body → **Script** → Ready to Film + Talent
- `pm.py apply-notion-comment --packet-file /path/to/packet.json` — Notion page comment → Script Revisions Needed
- `pm.py reaction --packet-file /path/to/reaction.json` — Slack ✅ approve (same body→Script path) / 📝 pickup / ❌
- `pm.py mve-packet --content-page-id ID [--footage-folder URL]`
- `pm.py status --event-key KEY`
- `pm.py resume-job --job-id ID --prompt-file /path/to/prompt.txt`
- `pm.py connections`
- `pm.py cold-test`
- `pm.py notion-confirm --intent-id ID --page-id ID [--url URL]`
- `pm.py notion-readback --intent-id ID --readback-file PATH`
- `pm.py reconcile-notion` / `pm.py reconcile [--dump-file PATH] [--fail-open]`
  - Notion Content Object **Status is source of truth** for stage. Brings local `objects.current_state` into line (imports Notion-only pages, rebinds phantom stub ids, reports mismatches). Silent (no Slack). Fail-closed by default.
- `pm.py delete-empty-junk [--object-id ID | --scan]` — delete empty junk Content Object shells (prefer delete over forever-BLOCKED). Silent.
- `pm.py match-footage [--content-id ID] [--drive-paths a,b] [--content-or-transcript-file PATH] [--footage-folder URL] [--required-files a,b] [--dry-run|--exec] [--submit-mve]`
- `pm.py send-shoot-batch` / `ensure-shoot-batch` — **DEPRECATED** no-ops (Shoot Batches retired)

The wrapper is the only interface the bot should use. It does not run ffmpeg, ffprobe, HyperFrames, or any media command. Tests use `--notion stub`. They never write real Notion pages and never post to Slack.

## Config

`/home/box/mansoor-content-operations/config/content-pm.json`

- Capture channel: `#sf-ideas-inbox` `C0BU7H12J4F`
- Delivery channel (bot scripts + videos): `#sf-scripts-ready-to-review` `C0BVC34H1MJ` (scripts) / `#sf-video-ready-to-review` `C0BVAAVASV7` (videos) / `#sf-ready-to-post` `C0BUTMAUTAB` (approved videos)
- Human content team (not AI deliverables): `#content-team` `C0BQKM27F5F`
- Model: `gpt-5.6-sol`
- Reasoning: `high`
- Host: this Linux VM (`cursor`)
- Skill registry: `config/skill-registry.json` version `2026-09-03.consolidation.2`
- System IDs: `config/system.json` (single authoritative copy)
- Idea Guy wrapper: `tools/idea-guy/idea_guy.py`
- SQLite: `state/content-pm.sqlite`

Event-driven only. Never cron. Never poll Slack.

## Registry

In-flight objects store the resolved registry version. Registry edits must not silently change in-flight work.

Scripted Talking Head has writer `mansoor-first-draft-writer` and editor `mansoor-talking-head-scripted-reels`. Sales Call Clip has editor `mansoor-sales-call-clips`. Genius Clip has editor `mansoor-genius-clips`. TOFU Copycat has writer `mansoor-tof-copycat-scout` and editor `mansoor-tof-copycat-editor`. Scripted Sales Call Skit, Scripted Roleplay, and Other Scripted Short remain `BLOCKED (missing skill reason)`. Missing writer or editor → `BLOCKED (missing skill reason)`. Do not substitute `general-video`. Idea work is sent to Idea Guy (`idea_guy.py`). Editing is sent to Master Video Editor (`mve.py`). Lifestyle Copycat review emoji loop stays with Eddie.

## Inbox root reactions (copycat-cutter)

Helper: `tools/content-os/inbox_reactions.py`. PM **never posts** reactions; it returns `inbox_reactions` Composio plans. Content Manager executes them as **`copycat-cutter`** only (never as Ivan / user-Slack). Scope: `#sf-ideas-inbox` `C0BU7H12J4F` **root idea messages** only — not `#sf-scripts-ready-to-review` deliverables.

### Exact emoji transition sequence
1. **`:eyes:`** — immediately on receive (`pm.py capture` start → stage `received`)
2. **`:writing_hand:`** — while processing; **remove `:eyes:`** when adding (`capture` finalize when `next_action` is `launch_analyzer` / writer; `apply_analysis` when launching writer → stage `processing`)
3. **`:white_check_mark:`** — draft ready / saved cleanly; remove eyes + writing_hand (`pm.py apply_draft` success → stage `success` / alias `draft_ready`)
4. **`:octagonal_sign:`** — BLOCKED; remove eyes + writing_hand (`apply_analysis` BLOCKED, reaction reject / missing playbook → stage `blocked`). Short BLOCKED reason still goes to Slack + Notion via existing shapes — no extra status spam.

Composio tools: `SLACKBOT_ADD_REACTION_TO_AN_ITEM` / `SLACKBOT_REMOVE_REACTION_FROM_ITEM` (account `copycat-cutter`). Each action is `fail_soft: true` — reaction API failures must not fail capture; attempts are logged under `logs/content-os/inbox-reactions.jsonl`.

CM routine: after `capture` / `apply-draft` / BLOCKED results, if `inbox_reactions.would_react`, run each action’s `composio_tool` + `composio_args` as copycat-cutter (or call `pm capture` which already stamps the plans).

## Slack notifications (fail-closed, no spam)

Outbound Slack is rare and ledger-gated. Helper: `tools/content-os/slack_identity.py` → `prepare_outbound` / `gated_send_decision`, backed by `tools/content-os/notifications.py` (`should_send` + `record_sent`). Wrapper entry: `pm.py gate-outbound` (never posts; dry-run only).

### Hard bans
- Never post the phrase **“Current status from the content bot”** (any casing).
- Never post intermediate processing states (“analyzing…”, “routing…”, “working on it…”, hop status, job IDs).
- user-Slack / `mansoor-slack` is **READ ONLY**. Never post as Ivan `U0BQJP0DEGH`.
- Write path: Composio Slackbot account **`copycat-cutter`** only (`U0BQGU4FVU5`).

### Allowed messages (routing LOCKED)
1. **Intake / idea thread** (`#sf-ideas-inbox`):
   - **One receipt**: `Got it — I saved this here: [Notion link]`
   - BLOCKED / clarify / pickup notes stay in the idea thread
2. **Bot deliverables** (top-level `#sf-scripts-ready-to-review` `C0BVC34H1MJ` (scripts) / `#sf-video-ready-to-review` `C0BVAAVASV7` (videos), account **`copycat-cutter`**, Ivan reacts in place):
   - Script ready / Script Needs Review → exact shape from `system.json` `script_delivery_format`:
     ```
     New Script ready for review
     Type: BOF Scripted Talking Heads / …
     Reference: (link)
     Script: (link)
     ```
   - Video Edit Ready for Review FILE posts (MVE)
3. **Human ops only** (`#content-team` `C0BQKM27F5F`): Drive sweeper “upload complete” — never dump AI scripts/videos here.

Never paste gold script text into Slack. Never post as Ivan. Never dump status into Eddie chat.
Helpers: `slack_identity.build_script_ready_outbound` / `build_idea_thread_outbound` → PM `slack_outbound` (never posts itself).

### Notification key
`slack:{channel_id}:{root_message_ts}:{notification_type}:{state_version}`

Duplicate keys are rejected (fail closed). Same blocker must never be sent twice.

### Silent background work
During **repairs / migrations / audits / restarts / backfills / reconciliation / reprocessing / bot instruction changes**: stay silent in Slack.
- Update Notion/SQLite silently; reprocess silently.
- If recovered → post ONLY the useful completed result (script-ready shape in `#sf-scripts-ready-to-review`, or idea-thread BLOCKED/receipt as appropriate).
- If still blocked for the same reason → post nothing.
- `reconcile-notion` always returns empty `slack_copy` / `would_post_slack=false`.

Modes that force silence unless recovered draft: `repair`, `audit`, `migrate`, `restart`, `backfill`, `reconcile`, `reprocess` (env `CONTENT_OS_SLACK_MODE` / `CONTENT_OS_MODE`).

### Who acquires sources
Grok (Eddie / Content Manager coordinator) may acquire + transcribe sources before dispatching Codex. The Grok dispatcher must still never spam status. Codex does the analysis/draft work; Content PM remains a dispatcher wrapper.

User-facing strings stay easy English. Never include job IDs, state codes, packet, dispatcher, validator, routing, workflow gap, or stack traces.

## Master Video Editor handoff

When Status is `Ready to Edit` and a scripted talking head has a gold script (page body / extras; optional Script property fallback) plus a footage folder, `mve-packet` prints a packet matching `config/example-job-packet.json`. Missing script → blocked, no packet. Call MVE only by printing the packet path. Do not invoke `mve.py submit` during cold tests.

## Codex launch (current CLI)

Same pattern as Master Video Editor. New session uses `codex exec`. Revisions resume the stored session id. Never start a new Codex task for a revision while the original session is accessible.

## Fail-closed

- `BLOCKED: CODEX DELEGATION UNAVAILABLE`
- `QUEUED: VM CAPACITY OR HOST UNAVAILABLE`
- `BLOCKED: REQUIRED CODEX SKILL UNAVAILABLE`
- `BLOCKED: REQUIRED CODEX MODEL UNAVAILABLE`
- `BLOCKED: ORIGINAL CODEX TASK UNAVAILABLE`
- `BLOCKED: SCRIPT MISSING`
- `BLOCKED: CONTENT OS DOES NOT INSPECT OR EDIT FOOTAGE`

## Not this bot

Does not watch folders, poll Drive, poll Slack, schedule recurring jobs, process footage, compete with Drive Sweeper, process Lifestyle Copycat, or create Grok bots or Slack listeners. Eddie owns live Slack and real Notion.


## Mansoor film queue (replaces Shoot Batches)

Do **not** create or use Shoot Batches in the active path. Every video remains one independent Content Object.

On Script Needs Review reactions in `#sf-scripts-ready-to-review` `C0BVC34H1MJ` (scripts) / `#sf-video-ready-to-review` `C0BVAAVASV7` (videos) (authorized reviewers allowlist; Ivan `U0BQJP0DEGH` + configurable teammates):

**✅ / `white_check_mark` — approve-as-is**
1. Extract gold script from Notion **page body** → set property **`Script`** (machine SoT)
2. Status → `Ready to Film` + **`Script Locked`=true**
3. Assign Talent = `Mansoor Alzayer` (Notion property `Talent`)
4. Object appears in Notion view **Film Next** via Status=Ready to Film + Pipeline=Scripted filter (no batch)
5. Do not create shoot batch rows / Notion Shoot Batch pages / `send-shoot-batch` for the active flow

**🧠 / `brain` — learn + approve** (Ivan hand-edited page body)
1. Diff current Notion page body vs prior bot draft (`bot_draft_script` / extras)
2. Write lessons into Content OS learning ledger targeting `mansoor-first-draft-writer` (+ voice/delivery rules via candidates/accepted-rules / RULES_LEARNED)
3. Ask clarifying questions in that Slack **thread** if needed (copycat-cutter; Slack only — quiet in Eddie chat)
4. Then same film lock as ✅ (body → Script → Ready to Film + Talent)
5. Thread voice notes after 🧠: STT then `pm.py learn-script-feedback --packet-file …`
6. Listener automation `script-brain-learn`: channel `#sf-scripts-ready-to-review`, emoji `brain`, **`bySelf: true`** (Ivan’s own reacts only)

Helper: `pm.py reaction` with emoji `brain` → `learn_approve`. ✅ mapping unchanged (`approve` → `sync_script_lock`).

Shoot Batches DB IDs remain in config for now but are hidden from active docs. The DB is not deleted.

`match-footage` matches landed footage to Ready to Film / filmed scripts waiting for edit.

Inputs: `--content-id` and/or `--drive-paths` (local folders/files; reads transcript sidecars only — never opens media) and/or a transcript/text/json file.

Behavior:
1. Score against Ready to Film (also Uploaded / Uploaded) via script/title similarity.
2. Low confidence or missing required media files → `ask_ivan` / clear blocker (no status advance).
3. High confidence → `Uploaded` → `Uploaded` → `Ready to Edit` (Notion Status updated when `--exec`).
4. Build validated Master Video Editor packet (`job_type` from format registry) and print `mve_packet_path` + `mve_submit_command`.
5. On handoff mark `Edit in Progress`. Default is **dry-run** (packet built for inspection; statuses not advanced; `mve.py submit` not invoked). Use `--exec` to advance; `--submit-mve` with `--exec` to hand the packet to the MVE wrapper (Codex may start — Grok never edits media).

Live Notion status enum uses `Edit in Progress` (not `IN_EDITING`).

## Notion ↔ SQLite status sync

Notion **Status** is the source of truth for Content Object stage. Local `objects.current_state` must match.

- Writes that set Status (capture block, analysis block, reaction, film-queue, footage match, etc.) update SQLite and emit Notion update actions (or stub writes).
- `notion-confirm` binds the real Notion page id onto the local row (rebinds phantom stub UUIDs).
- `notion-readback` mirrors Status into `current_state` when properties match.
- `reconcile` / `reconcile-notion --dump-file` repairs drift: import missing Notion pages, rebind phantoms by title, force Status→current_state, fail closed on remaining mismatches.

One-time repair example:

```
python3 tools/content-pm/pm.py reconcile --dump-file state/notion-content-objects-dump-2026-09-04.json
```

## Notion mode

`CONTENT_OS_NOTION_MODE=stub|actions` (default `actions` live; tests force `stub`).
Live mode emits `notion_actions` + `pending_notion` intents; does not claim Notion success from NotionStub.
Confirm with `notion-confirm`, then advance only after `notion-readback` matches expected properties.

## Inbox rules (fail-closed — 2026-09-04)

1. **TRANSLATE, never “wrong audience / not ICP”.** Idea Guy / analyzer must translate Ivan’s Slack note + reference into Mansoor’s ICP (licensed US life-insurance agent / Recruiter or Lone Wolf). Forbidden block reasons are rejected by `idea_guy.validate_output` and `apply-analysis`.
2. **Acquire from the link alone.** Never BLOCK asking Ivan to upload an Instagram video. On acquire failure: `next_action=retry_acquire`, silent Slack (no upload ask). Content Manager retries acquisition; Ivan will not upload.
3. **Empty junk Content Objects get deleted**, not parked forever as BLOCKED shells. Helper: `pm.py delete-empty-junk --object-id ID` or `--scan`. Capture deletes empty shells created when IG acquire fails.

## Instagram acquire

Grok (coordinator / acquire helpers) owns source acquisition. Codex never opens Instagram.

Acquisition order (fail closed; never invent transcript; **never ask Ivan to upload**):

1. Grok open public IG/YT ref
2. Sandcastles (if connected) for indexed transcript/analysis
3. Slack attachment / preview media on the idea thread
4. Local download + transcription (`tools/content-os/instagram_acquire.py` / `source_acquire.py` → evidence package)
5. **retry_acquire** from the same link (fail/retry). Never `ask_ivan_upload`.

Capture tooling writes a full **source evidence package** (original URL, Ivan’s exact note, source type, retrieval method/status, exact transcript, confidence, runtime, frames, hook/script verification flags) beside the transcript and passes it to Idea Guy. Analyzer packets that ask Codex to open an Instagram URL are rejected. Acquire failure → `ACQUIRE_RETRY` + delete empty junk Content Object shell + **empty** `slack_copy` (never ask for upload). Thread media/transcript replies resume the same Source/Object/session when real media exists. Background repairs stay silent unless `draft_ready`.


## Slack identity (fail-closed)

- Inbound read: `mansoor-slack` / user-Slack only.
- Outbound write: Composio Slackbot account `copycat-cutter` only (`U0BQGU4FVU5`).
- Never post as Ivan `U0BQJP0DEGH`.
- Never use user-Slack / mansoor-slack to send.
- Gate helper: `tools/content-os/slack_identity.py` — identity pre-send, notification ledger `should_send`, then Composio args; post-send verify; fail message: “I couldn’t send this from the content bot.”
- After a real successful send, call `record_outbound` / `notifications.record_sent`.
- No “Sent using @...” footers.
- No “Current status from the content bot” prefixes — ever.

## Script delivery + HYBRID lock (LOCKED)

Authoritative playbook: `SCRIPT_DELIVERY.md` (+ `HYBRID_SCRIPT_MODEL_LOCKED.md`). Gold format: `context/mansoor/GOLD_SCRIPT_FORMAT_mansoor-scripts-9_1.txt`.

**HYBRID:** During review, human SoT = Notion **page body** (never “Canonical Script”; never force Ivan into the tiny **Script** property). On Slack **✅** approve (or **Script Locked**), Content PM copies body → property **`Script`** for machines, then Ready to Film. MVE reads **Script** only after that copy. Gold line format: short title, then every spoken sentence on its own line. `apply-draft` writes body + lean props (`Script Locked`=false, Status, Hook, titles, Job ID…); Script property stays empty until approve.

### How Ivan locks or revises

1. Draft ready → Status **Script Needs Review**. Script text lives in the **page body**. Slack points him at the Notion page.
2. Ivan edits the **page body** (full editor). Notes = Notion comments.
3. Ivan reacts **✅** on Slack (or checks **`Script Locked`**).
4. Content PM `sync-script-lock` / `reaction(approve)`: extract body → set **`Script`** → **Script Locked**=true → Status **Ready to Film**, Talent=Mansoor. Learning pass runs when a prior revision note exists.
5. **Revision notes:** Ivan leaves a **Notion page comment** (and/or body edits). `apply-notion-comment` → **Script Revisions Needed**, resume same writer Codex session, overwrite **page body**, clear lock, back to **Script Needs Review**.
6. Slack 📝 = pickup for revisions (notes still in Notion). ❌ → **BLOCKED**.

### Video revise delivery gate (locked)
Before any revised video is posted back to Slack / marked ready for Ivan to review again:
1. Pull every open Frame note.
2. Fix each one.
3. Save a checklist in the job folder: each note → timestamp → fixed yes/no.
4. Check the whole video for that same kind of mistake.
5. Only if every note is fixed and Frame shows zero open notes → new Frame version + one Slack message with the link.
6. If any note is still open → do **not** post to Slack; keep status Edit Revisions Needed.

### Video naming for Ivan (locked)
Display name and file name = on-screen **Headline** only.
Not Working Title, not Notion Content title, not “Sales Call 04 …” labels.
When listing videos to Ivan in chat or Slack, lead with the headline.
When filing the finished `.mp4` into Drive Ready to Post, name the file from that same headline (safe characters only).

### Video ready to post handoff
On `#sf-video-ready-to-review` `C0BVAAVASV7`, authorized reviewer ✅ / `white_check_mark`:
1. Notion Status → **Ready to Post** (`pm.py reaction`).
2. File final into Drive `Ready to Post / {Month YYYY} / {DD} / {type}` via `tools/ready-to-post/ready_to_post.py` (America/Chicago; first day with funnel room: TOF≤6, MOF≤2, BOF≤2).
3. **Do not** post to `#sf-ready-to-post`. That channel is unused. Drive + Notion are enough.
4. Stay quiet in Grok Bot chat for day-to-day approvals. Not auto-publish.

### Locked type labels (funnel on the type — Drive + Slack review messages)
- `TOF Copy Cats`
- `TOF Static Reels`
- `MOF Genius Clips`
- `BOF Scripted Talking Heads`
- `BOF Sales Call Clips`
- `BOF Sales Call Skits`

Water buckets (locked): bank videos in Drive ahead of time. Each day TOF≤6, MOF≤2, BOF≤2 (max 10/day). Drop into the first Chicago day with room in that funnel. Use exact Type strings on Slack *review* messages (scripts / video review).


### Locked type labels (funnel on the type — Slack + Drive)
- `TOF Copy Cats`
- `TOF Static Reels`
- `MOF Genius Clips`
- `BOF Scripted Talking Heads`
- `BOF Sales Call Clips`
- `BOF Sales Call Skits`

Water buckets (locked): bank videos in Drive ahead of time. Each day TOF≤6, MOF≤2, BOF≤2 (max 10/day). Drop into the first Chicago day with room in that funnel. Use exact Type strings on every Slack delivery (scripts, video review, ready-to-post).

### SMM schedule (planned — not auto-publish yet)
Batch ahead, not daily drip. When days are banked in Drive, schedule **all unscheduled** files across those future days in one Post Bridge run (e.g. a week ≈ 70).
- Each file keeps its Chicago **day folder**; times only pick the clock inside that day.
- Window per day: **6:00am–7:00pm** America/Chicago.
- Human times: never :00 or :30; uneven minutes; ~45 min gaps when possible.
- Order within a day: TOF → MOF → BOF; filename A→Z inside a type.
- Skip anything already scheduled.
- Skill: mansoor-daily-post-bridge-schedule (+ mansoor-post-bridge-post).
- On ✅: file Drive + Notion only (no ready-to-post Slack). SMM/schedule program does **not** wake every morning just to schedule “today.”


### How CM detects approve vs notes

- Slack **✅** or Notion **`Script Locked`** → body→Script → film queue.
- Notion comments / Slack 📝 → revision path (inspect Notion first).
- Emoji is not the notes and not a second SoT.

Previous script version + Ivan note stay on object extras. One-video creative preferences are recorded only; never auto-universalized.

New Script Needs Review cards follow this. Old cards with property-only Script / Canonical Script: Content Manager migrates when touching them (copy into page body for review; ensure Script is populated on approve). Builder does not unblock or re-dispatch live cards.

See also: `learning/RULES_LEARNED.md`, Notion database **Rules Learned From Revisions** under Operation Mansoor, `config/skill-versions.json`.


## Content Object Status (authoritative 15-state list)

Exact names only — do not invent or rename:

1. Ideas for Review
2. Approved Ideas
3. Ready to Script
4. Script Needs Review
5. Script Revisions Needed
6. Ready to Film
7. Uploaded
8. Ready to Edit
9. Edit in Progress
10. Edit Ready for Review
11. Edit Revisions Needed
12. Ready to Post
13. Scheduled
14. Posted
15. BLOCKED

Missing skill/playbook is a **BLOCKED reason**, never a separate state.
BLOCKED always sets: Blocked Reason, What Is Needed, Who Can Resolve It, Date Blocked, Previous State.

### Reactions
- Script review (HYBRID):
  - Slack **✅** / Script Locked → approve-as-is: body→**Script** → Ready to Film + Talent
  - Slack **🧠** / `brain` → learn: body diff → write `mansoor-first-draft-writer/IVAN_LEARNED_RULES.md` + ledger → film lock; thread clarifying/voice via `learn-script-feedback`; automation `script-brain-learn` **bySelf true**
  - Notion comment → Script Revisions Needed; ❌ → BLOCKED
- Video review: ✅ → Notion Ready to Post + post same FILE block to `#sf-ready-to-post` `C0BUTMAUTAB` as copycat-cutter (+ revision learning); 📝 → Edit Revisions Needed (resume same editor Codex); ❌ → BLOCKED
- Idea discovery → Ideas for Review → human approval → Approved Ideas
- Intentional Ivan submit → Approved Ideas directly
- Film queue `Film Next`: Status = Ready to Film + Pipeline = Scripted

## Pipeline (format-specific paths)

Content Objects have a **Pipeline** select: `Scripted`, `Clipping`, `Copycat`, `Long Form`, `Other`.

| Format | Pipeline |
| --- | --- |
| Scripted Talking Head / skits / roleplays / Other Scripted Short | Scripted |
| Sales Call Clip / Genius Clip (exact skill) | Clipping |
| Lifestyle / TOFU Copycat | Copycat |
| YouTube / Live Training | Long Form |
| else | Other |

### Scripted path
Ideas for Review → Approved Ideas → Ready to Script → Script Needs Review (↔ Script Revisions Needed) → Ready to Film → Uploaded → Ready to Edit → Edit in Progress → Edit Ready for Review (↔ Edit Revisions Needed) → Ready to Post → Scheduled → Posted. BLOCKED anywhere.

### Clipping path
Raw recordings stay on **Content Sources only**. Sweeper: organize → transcribe → attach to Source → clip-selection → 0..N timestamped clips → one Content Object per clip linked to Source → start **Ready to Edit** → MVE with exact skill (`mansoor-sales-call-clips` / `mansoor-genius-clips`).

Allowed: Ready to Edit → Edit in Progress → Edit Ready for Review (↔ Edit Revisions Needed) → Ready to Post → Scheduled → Posted (+ BLOCKED).

**NEVER** on Clipping: Approved Ideas, Ready to Script, Script Needs Review, Script Revisions Needed, Ready to Film, Uploaded.

- ZERO-CLIP: keep Source, mark reviewed, 0 objects, no Slack.
- MULTI: 1 Source, N independent objects.
- DIRECT: timestamps given → Ready to Edit immediately after validation.
- Gate before Ready to Edit: source, start, end, speaking arc, content type, exact edit skill, assigned editor, source relation — else BLOCKED.

Validators reject illegal transitions per Pipeline. Missing skill = BLOCKED reason, never a state.

### Reactions (same Content Object + Notion + SQLite + same Codex session; no duplicates)
- Script (HYBRID): ✅/Script Locked → body→Script → Ready to Film; Notion comment → Script Revisions Needed; ❌ → BLOCKED
- Video Slack (`#sf-video-ready-to-review`): ✅ → Ready to Post + copy FILE post into `#sf-ready-to-post` `C0BUTMAUTAB` + learning/skill-hardening; 📝 → Edit Revisions Needed (same editor Codex); ❌ → BLOCKED

NO Slack status spam. NO media edits by Grok. NO invented statuses.


## Inbox reaction protocol (LOCKED)
On `#sf-ideas-inbox` root idea messages, Content Manager executes `inbox_reactions` from PM results as **copycat-cutter** (never Ivan):
1. `eyes` immediately on receive
2. remove `eyes` + add `writing_hand` while processing
3. remove prior + add `white_check_mark` when successfully processed (draft ready / saved cleanly)
4. remove prior + add `octagonal_sign` when BLOCKED (+ short reason Slack/Notion)

PM returns `inbox_reactions.actions[]` with Composio `SLACKBOT_ADD_REACTION_TO_AN_ITEM` / `SLACKBOT_REMOVE_REACTION_FROM_ITEM`. Fail soft if a remove misses. Deliverables still go to `#sf-scripts-ready-to-review`.

- **Bulk post lock:** one Slack message per Content Object in `#sf-scripts-ready-to-review`. Never combine multiple scripts/videos into one large message.


## #sf-scripts-ready-to-review delivery shapes (LOCKED)
Scripts (top-level, one message per item):
```
New Script ready for review
Type: …
Reference: <original Instagram/source video URL — NEVER Notion>
Script: <Notion content page URL>
```
Videos (top-level, one message per item, **no Script line**):
- Sales Call Clip: `TYPE` + `PLATFORM` + `Headline:` (on-screen text, not Title) + `FILE`
- BOF Scripted Talking Heads: `TYPE: BOF Scripted Talking Heads` + `PLATFORM` + `Headline:` + `FILE`

## Inbox wake finalize (fail-closed — 2026-09-05)
Main inbox wakes must end with `pm.py wake-finalize --packet-file …`.
- ok only for **draft_ready** or **complete BLOCKED**
- otherwise forces Notion BLOCKED + Slack 🛑 (`octagonal_sign`) + short idea-thread reason + event `failed`/`INCOMPLETE_WAKE`
- Prevents silent eyes-only / plan-only / fake status=ok drops
- Eyes-only automation must not call wake-finalize
