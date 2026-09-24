https://app.notion.com/p/3d099a426f998102b138c16bea752ff5?pvs=204

Here is the result of "fetch" for the Page with URL https://app.notion.com/p/3d099a426f998102b138c16bea752ff5 as of 2026-09-03T07:04:03.533Z:
<page url="https://app.notion.com/p/3d099a426f998102b138c16bea752ff5" icon="🧠">
<ancestor-path>
<parent-page url="https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01" title="Mansoor Content OS — Control Plane"/>
<ancestor-2-page url="https://app.notion.com/p/3be99a426f9981a8a423c2b66e0bf965" title="Operation Mansoor"/>
</ancestor-path>
<properties>
{"title":"AI Implementation Contract — Mansoor Content OS"}
</properties>

<content>
<callout icon="🧠" color="purple_bg">
	**Audience:** Grok Bot, Codex, future AIs, and engineers extending the system.
</callout>
# Authority order
1. Explicit current instruction from Ivan
2. This implementation contract
3. Linked worker build prompts and registered skills
4. Existing Operation Mansoor SOPs
5. Conservative fail-closed behavior
# Stable identifiers
- Slack capture channel ID: `C0BU7H12J4F` (current name `#content-ideas-inbox`, private)
- Slack delivery channel ID: `C0BQKM27F5F`
- Ivan: `U0BQJP0DEGH`
- Mansoor: `U0BQGPXNWCA`
- Content Sources database: `527c4746637e4cff9c4dc06c59ce255d`
- Content Sources data source: `33c6a192-c09e-40f6-a450-92ca05c77511`
- Content Objects database: `8439d827f39b4c47acd9e17271045038`
- Content Objects data source: `b70abe56-526c-4189-85d4-8983e3e65966`
- Shoot Batches database: `a36b0d0b40ec49a787d4df63ab90ef40`
- Shoot Batches data source: `8ae3a3d3-9be5-4f6f-b90c-cf18fbb74405`
- Linux workspace: `/home/box/mansoor-content-operations`
- Master Video Editor wrapper: `/home/box/mansoor-content-operations/tools/master-video-editor/mve.py`
# Core invariants
- One publishable video equals one Content Object.
- One Source may relate to zero, one, or many Content Objects.
- Preserve the raw event/source. Normalization is additive.
- Human titles and structured intake are optional.
- Grok dispatchers do not perform worker tasks.
- Codex workers use explicit skills and store their session IDs.
- Same object revision resumes the same Codex session.
- No registered exact-match playbook means `NEEDS_PLAYBOOK`.
- Never silently use a similar skill.
- Every external write is idempotent and auditable.
# Event contracts
## Slack idea capture
Key: `slack:{channel_id}:{message_ts}`
Required payload: channel ID, message timestamp, sender ID, text, files, links, thread status, event subtype, and permalink.
Only root human messages in `C0BU7H12J4F` are eligible. Ignore bot messages and duplicates.
## Analyzer job
Key: `analyze:{source_page_id}:v{analysis_version}`
Must persist job ID, packet hash, status, attempt, Codex session ID, output hash, timestamps, and blocker.
## Writer job
Key: `write:{content_page_id}:v{draft_version}`
Must persist the same fields. JSON canonical script and Notion canonical script must match.
## Edit job
Uses the existing Master Video Editor packet and registry. The PM must not call Codex for editing directly.
# Routing behavior
- Clear or unlabeled current idea/reference → default Scripted Talking Head → analyze → draft automatically.
- Scripted Sales Call Skit, Scripted Roleplay, TOFU Copycat, or Other Scripted Short → analyze → IDEA_REVIEW.
- Sales Call or Genius Call source → analyze → zero or more timestamped clip objects.
- Unknown exact workflow or missing skill → NEEDS_PLAYBOOK.
# Reaction behavior
Reactions are event-driven. Do not poll.
## Idea-analysis message
- ✅ from Ivan: approve the idea, resolve the registered writer, move to DRAFTING, and launch it.
- 📝 from Ivan: fetch thread/Notion notes and resume analyzer session.
- ❌ from Ivan: ARCHIVED; cancel unstarted downstream jobs.
## Script-review message
- ✅ from Ivan: READY_TO_FILM.
- 📝 from Ivan: fetch notes and resume writer session.
- ❌ from Ivan: ARCHIVED.
## Video-review message
Use the existing Master Video Editor reaction listener and [Frame.io](http://Frame.io) revision contract.
# Minimum SQLite tables
- `events`: event_key, provider, payload_hash, raw_payload, first_seen_at, handled_at, status, error
- `objects`: notion_page_id, object_type, source_page_id, content_page_id, current_state, updated_at
- `jobs`: job_id, job_type, object_id, packet_hash, codex_session_id, status, attempt, started_at, finished_at, blocker
- `transitions`: object_id, from_state, to_state, trigger, actor, timestamp, metadata_json
- `deliveries`: object_id, slack_channel_id, root_ts, frame_url, delivery_state, updated_at
# Atomicity
Use a local intent record before any Notion or Slack mutation. After each external write, persist the returned ID immediately. On retry, read state and continue from the first incomplete step. Never repeat a successful write because a later step failed.
# Skill registry
Every route must resolve:
- content format,
- analyzer prompt version,
- writer skill/workflow,
- editor skill,
- required inputs,
- output validator,
- approval gate,
- downstream dispatcher.
Registry entries are versioned. An object stores the resolved version. Registry changes do not silently alter in-flight work.
# Required observability
Every object must answer:
- where it came from,
- what format it is,
- what state it is in,
- what is blocking it,
- which worker owns the next action,
- which Codex session holds context,
- what was delivered and where,
- what skill/version was used.
# Extension procedure
To add a new format:
1. Capture and analyze real examples.
2. Define its object fields and state transitions.
3. Create the writer/editor playbook with measurable quality gates.
4. Add it to the registry.
5. Add packet and output validators.
6. Add cold tests, including failure and revision.
7. Activate routing only after tests pass.
8. Clear NEEDS_PLAYBOOK objects individually after confirming compatibility.
# Linked specifications
- <mention-page url="https://app.notion.com/p/3d099a426f998172a70bc24d6783917a"/>
- <mention-page url="https://app.notion.com/p/3d099a426f99812684e8e5a6623416e9"/>
- <mention-page url="https://app.notion.com/p/3d099a426f9981b291a9ea4d2d15db31"/>
- <mention-page url="https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01">Mansoor Content OS — Control Plane</mention-page>
# Private-channel membership
Slack bots cannot read or post in this private channel merely because their workspace connection is active. Before activation, add the Mansoor Content PM bot/app and the bot identity used for acknowledgements to `C0BU7H12J4F`. Verify each identity can read one test event and post one thread reply. A `channel_not_found` response from the bot identity is an access failure, not evidence that the channel ID is wrong.
# User-facing language contract
Slack copy is a presentation layer for humans. It must use short, everyday English and one clear next action. Never expose internal architecture words, enum values, job IDs, packet names, validation terms, database IDs, stack traces, or raw provider errors. Store those in Notion and SQLite.
</content>
</page>
