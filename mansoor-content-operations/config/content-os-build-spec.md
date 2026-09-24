# Mansoor Content OS — implement now

Build the control plane on this Linux machine. Do not process footage, upload media, or post a delivery video.

Workspace: `/home/box/mansoor-content-operations`
Do NOT modify Master Video Editor (`tools/master-video-editor/`, `state/master-video-editor.sqlite`, `MASTER_VIDEO_EDITOR.md`).
Do NOT modify Drive Sweeper or Lifestyle Copycat.

Reuse Codex launch patterns from `tools/master-video-editor/mve.py` (`launch_codex`, `parse_jsonl_session`, model `gpt-5.6-sol`, reasoning `high`). Copy those helpers rather than importing mve.py if that would couple them.

## Stable IDs

- Slack capture: `C0BU7H12J4F` (#sf-ideas-inbox, private)
- Slack delivery (bot): `C0BVC34H1MJ` (#sf-scripts-ready-to-review)
- Human content team: `C0BQKM27F5F` (#content-team)
- Ivan: `U0BQJP0DEGH`
- Mansoor: `U0BQGPXNWCA`
- Content Sources DB: `527c4746637e4cff9c4dc06c59ce255d` collection `33c6a192-c09e-40f6-a450-92ca05c77511`
- Content Objects DB: `8439d827f39b4c47acd9e17271045038` collection `b70abe56-526c-4189-85d4-8983e3e65966`
- Shoot Batches DB (legacy / historical; keep IDs, not used in active film queue — use Mansoor — Film Next): `a36b0d0b40ec49a787d4df63ab90ef40` collection `8ae3a3d3-9be5-4f6f-b90c-cf18fbb74405`
- Codex project id: `fe9995a5-fed7-46f3-92db-221e0cb79ebc`
- Host: `cursor`
- Slack team: `T0BQLF8P4AY`
- Slackbot alias (when invited): `copycat-cutter` — do not call Slack from tests
- MVE wrapper: `/home/box/mansoor-content-operations/tools/master-video-editor/mve.py`

## Notion property names (exact)

### Content Sources
title: Source
select Source Type: Instagram Reference | Sandcastles | Uploaded Reference | Voice Note | Sales Call | Genius Call | YouTube | Slack Note | Other
url: Source URL
text: Slack Channel ID, Slack Message TS, Notes, Analysis Job ID
date: Capture Date
select Analysis Status: Queued | Analyzing | Analyzed | Blocked
url: Transcript Link

### Content Objects
title: Content
select Format: Scripted Talking Head | Scripted Sales Call Skit | Scripted Roleplay | TOFU Copycat | Other Scripted Short | Sales Call Clip | Genius Clip | Lifestyle Copycat | YouTube | Live Training
select Status: Ideas for Review | SOURCE_ANALYZING | Ideas for Review | BLOCKED (missing skill reason) | DRAFTING | Script Needs Review | REVISION_NEEDED | Ready to Film | SENT_TO_MANSOOR | FILMED | FOOTAGE_MATCHING | Ready to Edit | EDITING | Edit Ready for Review | Edit Revisions Needed | APPROVED | READY_TO_POST | Posted | BLOCKED | ARCHIVED
relation Source → Content Sources collection
relation Shoot Batch → Shoot Batches (legacy; active path uses Talent + Ready to Film / Mansoor — Film Next)
text: Working Title, Hook, Angle, Premise, Why It May Work, Script, Required Workflow, Skill Gap, Blocker, Job ID, Codex Thread ID, Slack Delivery TS
checkbox: Script Locked (Notion-first lock; CM watches this — Slack ✅ optional backup)
number: Draft Version, Routing Confidence
select Edit Skill: mansoor-talking-head-scripted-reels | mansoor-sales-call-clips | long-form-clip-selector | general-video
multi_select Platforms: Instagram | YouTube Shorts | YouTube | LinkedIn
select Priority: Urgent | High | Normal | Low
url: Drive Folder, Footage Link, Frame Link, External Audio Link

Never set Edit Skill to general-video as a fallback.

## Files to create

### Content PM
- `/home/box/mansoor-content-operations/CONTENT_PM.md`
- `/home/box/mansoor-content-operations/config/content-pm.json`
- `/home/box/mansoor-content-operations/config/skill-registry.json`
- `/home/box/mansoor-content-operations/tools/content-pm/pm.py` (executable)
- `/home/box/mansoor-content-operations/tests/content-pm/` fixtures + `test_pm.py`

SQLite created at runtime: `/home/box/mansoor-content-operations/state/content-pm.sqlite`

### Idea Analyzer
- `/home/box/mansoor-content-operations/IDEA_ANALYZER.md`
- `/home/box/mansoor-content-operations/config/idea-analyzer.json`
- `/home/box/mansoor-content-operations/tools/idea-analyzer/analyzer.py`
- `/home/box/mansoor-content-operations/tools/idea-analyzer/schema.py`
- `/home/box/mansoor-content-operations/tools/idea-analyzer/prompt.md`
- `/home/box/mansoor-content-operations/tools/idea-analyzer/fixtures/` (accessible text, inaccessible link, clips, zero-candidate)
- `/home/box/mansoor-content-operations/tests/idea-analyzer/test_analyzer.py`

### First Draft Writer
- `/home/box/mansoor-content-operations/FIRST_DRAFT_WRITER.md`
- `/home/box/mansoor-content-operations/config/first-draft-writer.json`
- `/home/box/mansoor-content-operations/tools/first-draft-writer/writer.py`
- `/home/box/mansoor-content-operations/tools/first-draft-writer/schema.py`
- `/home/box/mansoor-content-operations/tools/first-draft-writer/prompt.md`
- `/home/box/mansoor-content-operations/tools/first-draft-writer/fixtures/`
- `/home/box/mansoor-content-operations/tests/first-draft-writer/test_writer.py`

### Shared
- `/home/box/mansoor-content-operations/tools/content-os/db.py` (SQLite schema)
- `/home/box/mansoor-content-operations/tools/content-os/codex_launch.py` (shared Codex exec/resume)
- `/home/box/mansoor-content-operations/tools/content-os/notion_stub.py` (file-backed fake Notion for tests)
- `/home/box/mansoor-content-operations/tools/content-os/validators.py`
- `/home/box/mansoor-content-operations/config/content-os-readiness.json` written after tests

## SQLite (content-pm.sqlite)

Tables required by contract:
- events(event_key PRIMARY KEY, provider, payload_hash, raw_payload, first_seen_at, handled_at, status, error)
- objects(object_id PRIMARY KEY, notion_page_id, object_type, source_page_id, content_page_id, current_state, updated_at)
- jobs(job_id PRIMARY KEY, job_type, object_id, packet_hash, codex_session_id, status, attempt, started_at, finished_at, blocker)
- transitions(id, object_id, from_state, to_state, trigger, actor, timestamp, metadata_json)
- deliveries(object_id, slack_channel_id, root_ts, frame_url, delivery_state, updated_at)

Also add:
- intents(intent_id, event_key, step, payload_json, result_json, status, created_at) — local intent before any external write
- unique indexes: events.event_key, jobs.job_id, jobs.packet_hash where useful

Idempotency:
1. Write intent row first
2. After each external write, persist returned ID immediately
3. On retry, continue from first incomplete step
4. Never repeat a successful write

event_key = `slack:{channel_id}:{message_ts}`
analyze job_id = `analyze:{source_page_id}:v{analysis_version}`
write job_id = `write:{content_page_id}:v{draft_version}`

## Skill registry (versioned)

File `config/skill-registry.json` version `2026-09-03.1`.

Entries:

1. Scripted Talking Head
   - analyzer_prompt_version: idea-analyzer-v1
   - writer_workflow: mansoor-first-draft-writer
   - editor_skill: mansoor-talking-head-scripted-reels (path `/home/box/.codex/skills/mansoor-talking-head-scripted-reels/SKILL.md`)
   - approval_gate after draft: Script Needs Review
   - auto_draft: true
   - downstream: first-draft-writer then later MVE job_type scripted_talking_head

2. Scripted Sales Call Skit
   - writer_workflow: null (missing)
   - editor_skill: null (do NOT use general-video)
   - auto_draft: false
   - after analysis: if missing writer or editor → BLOCKED (missing skill reason)

3. Scripted Roleplay — same, missing both → BLOCKED (missing skill reason)

4. TOFU Copycat — missing writer/editor (Lifestyle Copycat is a different system) → BLOCKED (missing skill reason)

5. Other Scripted Short — missing → BLOCKED (missing skill reason)

6. Sales Call Clip
   - writer_workflow: null (clips, no script writer)
   - editor_skill: mansoor-sales-call-clips
   - auto_draft: false
   - after analysis: create clip objects, later MVE job_type sales_call_clip
   - writer not required for clips; editor required. If editor missing → BLOCKED (missing skill reason). Editor exists so clip objects may proceed toward edit when footage exists.

7. Genius Clip
   - editor_skill: long-form-clip-selector — THIS SKILL FILE DOES NOT EXIST on disk (only the Notion option exists). Treat as missing → BLOCKED (missing skill reason). Do not substitute mansoor-sales-call-clips.

An in-flight object stores the resolved registry version. Registry edits must not silently change in-flight work.

## pm.py CLI

```
pm.py init
pm.py capture --packet-file PATH [--notion stub|plan]
pm.py apply-analysis --packet-file PATH
pm.py apply-draft --packet-file PATH
pm.py reaction --packet-file PATH
pm.py mve-packet --content-page-id ID [--footage-folder URL]
pm.py match-footage [--content-id ID] [--drive-paths a,b] [--dry-run|--exec] [--submit-mve]
pm.py gate-outbound --channel ID --text '...' --type TYPE --state-version V --root-ts TS [--mode reprocess]
pm.py status --event-key KEY
pm.py resume-job --job-id ID --prompt-file PATH
pm.py connections
pm.py cold-test
pm.py send-shoot-batch / ensure-shoot-batch  # DEPRECATED no-ops (Film Next replaces Shoot Batches)
```

`--notion stub` uses file-backed fake pages under `/tmp` or `tests/content-pm/notion-stub/` (never real Notion from tests).

`capture` packet:
```json
{
  "channel_id": "C0BU7H12J4F",
  "message_ts": "123.456",
  "sender_id": "U0BQJP0DEGH",
  "text": "...",
  "files": [],
  "links": [],
  "is_thread_reply": false,
  "event_subtype": "message",
  "permalink": "https://mvp-agency.slack.com/archives/C0BU7H12J4F/p...",
  "is_bot": false
}
```

Ignore if: wrong channel, is_bot, is_thread_reply (unless explicit revision command), duplicate event_key already handled.

Source type detection:
- instagram.com / instagr.am → Instagram Reference
- sandcastles / sandcastle → Sandcastles
- youtube.com / youtu.be → YouTube
- optional labels override: `[talking-head]` `[sales-skit]` `[tofu-copycat]` `[sales-call]` `[genius]` `[roleplay]`
- voice note file → Voice Note
- unlabeled idea/reference default format Scripted Talking Head, source Slack Note or Instagram/YouTube from URL

Working title: generate from first ~8 words or domain of URL. Do not require Ivan to name it.

Routing confidence 0-1. If < 0.65 AND a wrong choice would change the workflow (e.g. sales-call vs talking-head unclear), return slack_copy asking one short clarification and set BLOCKED / AWAITING_FORMAT_CLARIFICATION. Do not ask when unlabeled default talking-head is safe.

Sales Call / Genius source: create Source only (no Content Object yet).

Slack copy (user-facing, stored in result `slack_copy`, never posted by tests):
- idea: `Got it — I saved this here: {content_object_url}`
- source-only: `Got it — I saved the source here: {source_url}`
- needs playbook: `I saved this, but we do not have instructions for making this type of video yet: {notion_url}`
- draft ready: `Your draft is ready to review: {content_object_url}`
Never include job IDs, state codes, packet, dispatcher, validator, routing, workflow gap, stack traces.

`capture` returns JSON with: event_key, notion_plan (properties to write), created stub ids, next_action (launch_analyzer|await_clarification|ignore), slack_copy.

After analysis (`apply-analysis` with validated analyzer JSON):
- talking-head + writer+editor present → Status DRAFTING, next_action launch_writer
- skit/tofu/roleplay + skills present → Ideas for Review, wait for Ivan ✅
- any format missing writer or editor when those are required → BLOCKED (missing skill reason)
- sales/genius: create one object per accepted clip_candidate; zero candidates is valid

Reaction packet:
```json
{"channel_id":"C0BU7H12J4F","message_ts":"...","user_id":"U0BQJP0DEGH","emoji":"white_check_mark"}
```
Only Ivan. Ideas for Review message: ✅ launch writer if registry allows else BLOCKED (missing skill reason); 📝 resume analyzer; ❌ ARCHIVED. Script Needs Review: primary lock = Notion Script Locked → Ready to Film + Talent=Mansoor (Film Next; no Shoot Batch). Optional Slack ✅ same path; 📝 / Notion comment → resume writer; ❌ ARCHIVED/BLOCKED.

`mve-packet`: if Status Ready to Edit and scripted talking head has Script and footage folder, emit exact MVE JSON matching example-job-packet.json. Missing script → BLOCKED, do not emit. Call MVE only via printing the packet path; do not invoke mve.py submit during cold tests unless `--dry-run`.

## analyzer.py CLI

```
analyzer.py validate --packet-file PATH
analyzer.py submit --packet-file PATH [--dry-run]
analyzer.py resume --job-id ID --prompt-file PATH
analyzer.py validate-output --output-file PATH
```

Input packet required keys: job_id, source_page_id, source_type, source_url, slack_channel_id, slack_message_ts, capture_text, content_object_id (nullable)

`--dry-run` builds Codex command + prompt, does not exec Codex.

Output JSON contract exactly as Notion build prompt. schema.py validates required fields, clip timestamps HH:MM:SS.mmm when clip_candidates nonempty, writer_workflow_available/editor_skill_available booleans.

For tests, allow `--fixture-output PATH` to ingest a canned analyzer JSON as if Codex returned it (no Codex). Duplicate job_id is a no-op returning existing job.

## writer.py CLI

Same pattern. Input packet required: job_id, content_page_id, source_page_id, format (must be Scripted Talking Head for this writer), working_title, analysis, revision_request.

Reject if format is not Scripted Talking Head (that is BLOCKED (missing skill reason), not this writer).

Quality gates in schema.py:
- canonical_script nonempty
- claims_checked is true
- filming_lines nonempty complete sentences
- if cta looks like a keyword, must be CAPITALS inside quotes e.g. `"BLUEPRINT"`
- JSON canonical_script/script must equal notion_script (Notion Script field); gold line format required

`--fixture-output` for tests.

## Codex proof (required)

Run ONE tiny harmless Codex session (no media):

```
codex exec --skip-git-repo-check --json -m gpt-5.6-sol -c 'model_reasoning_effort="high"' \
  -C /home/box/mansoor-content-operations/jobs/content-os-codex-proof \
  --approve-for-me --thread-source content-os-proof \
  -o .../codex-last-message.txt \
  'Reply with exactly: CONTENT-OS-PROOF-OK'
```

Then resume the SAME session_id with: `Reply with exactly: CONTENT-OS-PROOF-RESUME-OK`

Save session_id + both last messages to `/home/box/mansoor-content-operations/config/codex-proof.json`.
Timeout 180s each. If Codex fails, record the exact error; do not fake success.

## Tests (pytest or a self-contained python runner)

`pm.py cold-test` must run all of these with NOTION stub, no Slack, no footage:

PM:
1. Slack idea event → one Source + one Content Object
2. Duplicate event → nothing new
3. Instagram link → source type Instagram Reference, next_action launch_analyzer
4. Talking-head analyzer success → DRAFTING + launch_writer
5. Future format (sales-skit labeled) after analysis with missing writer → BLOCKED (missing skill reason) not writer
6. Sales call analyzer zero candidates → source only, no objects
7. Sales call analyzer two clip candidates → two content objects
8. Failed Notion write (stub raises after intent) → retryable, no duplicate on second apply
9. Ready to Edit with script + footage → valid MVE packet (do not submit)
10. Ready to Edit missing script → block, no packet
11. Stored Codex session resume command uses same session id (unit-level; plus the real proof above)
12. Unknown roleplay → BLOCKED (missing skill reason), does not dispatch writer or MVE
13. Grok-refusal helper: `pm.py connections` or a function `refuse_media_work()` returns the fail-closed string if asked to edit/inspect footage

Analyzer tests:
- accessible text fixture validates
- inaccessible link output status BLOCKED accepted
- duplicate job ID no second job
- one-to-many clip output
- zero-candidate source
- same-session repair command uses stored session id

Writer tests:
- first draft fixture validates
- unsupported claim (claims_checked false) rejected
- CTA keyword must be `"BLUEPRINT"` style
- Notion equality (json vs notion_canonical_script)
- duplicate job ID
- same-session revision

Write results to `/home/box/mansoor-content-operations/config/content-os-test-results.json` with each test name pass/fail/error.

## Docs

CONTENT_PM.md, IDEA_ANALYZER.md, FIRST_DRAFT_WRITER.md in the same voice as MASTER_VIDEO_EDITOR.md: dispatcher only, wrapper commands, fail-closed, not this bot.

## Python

Python 3.12, stdlib only (no pip). pytest is optional; a `python3 tests/.../test_pm.py` self-runner is fine.

## Report back

Return:
- list of files created
- exact tests passed/failed
- path to test-results json
- Codex proof session_id and whether resume used the same id
- any blockers
- do NOT create Grok bots, Slack listeners, or real Notion pages (Eddie does that)
- do NOT post to Slack

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
- Script review: ✅ → Ready to Film; 📝 → Script Revisions Needed (resume same writer Codex session); ❌ → BLOCKED
- Video review: ✅ → Ready to Post (+ revision learning); 📝 → Edit Revisions Needed (resume same editor Codex); ❌ → BLOCKED
- Idea discovery → Ideas for Review → human approval → Approved Ideas
- Intentional Ivan submit → Approved Ideas directly
- Film queue `Mansoor — Film Next`: Status = Ready to Film + Pipeline = Scripted

## Inbox fail-closed rules (2026-09-04)

- Analysis/first-draft: TRANSLATE into Recruiter or Lone Wolf; never Block “wrong audience / not ICP”.
- Acquisition: get reel from link alone; fail/retry; never Block asking Ivan to upload.
- Empty junk Content Objects: delete, do not park forever as BLOCKED shells.
