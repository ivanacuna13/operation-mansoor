https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01?pvs=204

Here is the result of "fetch" for the Page with URL https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01 as of 2026-09-03T07:08:31.850Z:
<page url="https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01" icon="🎛️">
<ancestor-path>
<parent-page url="https://app.notion.com/p/3be99a426f9981a8a423c2b66e0bf965" title="Operation Mansoor"/>
</ancestor-path>
<properties>
{"title":"Mansoor Content OS — Control Plane"}
</properties>

<content>
<callout icon="🎯" color="blue_bg">
	**Purpose:** Turn every committed idea into one trackable content object, a source-grounded first draft, filmed footage, a correctly routed Codex edit, review, and publication.
</callout>
# System boundaries
- **Notion** is the human-facing source of truth for ideas, scripts, status, and links.
- **Slack** is the mobile capture, notification, and review surface. The capture channel can hold multiple idea formats.
- **Google Drive** stores source footage, audio, drafts, and final assets.
- **SQLite on the Linux machine** stores dispatcher state, idempotency keys, retries, job ownership, and Codex session IDs.
- **Grok bots** dispatch and communicate. They do not analyze, write, edit, upload, or perform media work themselves.
- **Codex workers** perform analysis, writing, editing, QC, [Frame.io](http://Frame.io) delivery, and revision work.
# Canonical databases
- <mention-database url="https://app.notion.com/p/527c4746637e4cff9c4dc06c59ce255d">Content Sources</mention-database> — one row per raw reference or recording.
- <mention-database url="https://app.notion.com/p/8439d827f39b4c47acd9e17271045038">Content Objects</mention-database> — one row per publishable video.
- <mention-page url="https://app.notion.com/p/a36b0d0b40ec49a787d4df63ab90ef40"/> — filming handoffs for approved scripts.
# Capture rule
The private Slack channel **#content-ideas-inbox** with channel ID `C0BU7H12J4F` is the shared idea entry point. Every eligible root message creates a Source and at least one Content Object. For the current **Scripted Talking Head** format, analysis and first-draft writing run automatically. Future formats such as **Scripted Sales Call Skit** and **TOFU Copycat** are captured and analyzed, then stop at `IDEA_REVIEW` until Ivan approves them.
# Object rules
1. One publishable video equals one Content Object.
2. One source may create multiple Content Objects.
3. Scripted ideas create one Content Object immediately.
4. Sales calls and Genius recordings create a Source first; screening may create zero or more separate clip objects.
5. Human titles are optional. The PM generates a short working title and Notion assigns the permanent ID.
6. The full canonical script lives in the Content Object page body under **Canonical Script**. The property mirrors it when it fits.
7. Separate Google Docs are not required.
# Scripted workflow
`IDEA_CAPTURED → SOURCE_ANALYZING → DRAFTING → SCRIPT_REVIEW → REVISION_NEEDED or READY_TO_FILM → SENT_TO_MANSOOR → FILMED → FOOTAGE_MATCHING → READY_TO_EDIT → EDITING → READY_FOR_REVIEW → EDIT_REVISIONS or APPROVED → READY_TO_POST → PUBLISHED`
# Source-first workflow
Sales call or Genius source → analysis and clip screening → zero or more Content Objects → `READY_TO_EDIT`.
# Required idempotency
- Slack capture: `slack:{channel_id}:{message_ts}`
- Source analysis: `analyze:{source_page_id}:v{analysis_version}`
- First draft: `write:{content_page_id}:v{draft_version}`
- Edit: use the Master Video Editor `job_id`
- Revision: resume the stored Codex session; never create a new session for the same revision chain.
# Failure behavior
- Fail closed if the source cannot be accessed, the Notion write fails, the worker output does not validate, or required footage/script fields are missing.
- Record the exact blocker in Notion and SQLite.
- Never silently skip, duplicate, or invent source content.
- Never allow a Grok dispatcher to do the worker's work itself.
# Slack language
Every Slack message must use short, everyday English. Never expose terms such as routing, object, dispatcher, workflow gap, state codes, job IDs, idempotency, validators, or stack traces.
Use messages like:
- `Got it — I saved this here: [link]`
- `Your draft is ready to review: [link]`
- `I analyzed this idea. Approve it if you want me to write the draft: [link]`
- `I need one detail before I can continue: [short question]`
- `I saved this, but we do not have instructions for making this type of video yet: [link]`
Technical detail belongs in Notion and SQLite. No extra chatter is posted to the channel.
# Instagram capture
Use the phone Share Sheet to send an Instagram reference into **#content-ideas-inbox**. Do not scrape or poll Ivan's private Instagram Saves collection.
<page url="https://app.notion.com/p/3d099a426f998172a70bc24d6783917a">Build Prompt — Mansoor Content PM</page>
<page url="https://app.notion.com/p/3d099a426f99812684e8e5a6623416e9">Build Prompt — Mansoor Idea Analyzer</page>
<page url="https://app.notion.com/p/3d099a426f9981b291a9ea4d2d15db31">Build Prompt — Mansoor First Draft Writer</page>
# How to submit ideas
Send ideas raw. Any of these are valid:
- an Instagram, YouTube, or other reference link,
- a screenshot or uploaded reference video,
- a voice note,
- a rough sentence,
- a link plus a short note about what is interesting.
No title, Notion link, template, or structured fields are required.
## Optional routing labels
Add one only when you want to force a format:
- `[talking-head]`
- `[sales-skit]`
- `[roleplay]`
- `[tofu-copycat]`
- `[sales-call]`
- `[genius]`
Without a label, the PM infers the format and records its confidence. During the current phase, ambiguous idea/reference messages default to **Scripted Talking Head**. If the choice would materially change the work and confidence is low, the PM asks one short question in the message thread.
## What the PM normalizes
The raw message is preserved unchanged. The PM adds:
- generated working title,
- source type and canonical link,
- intended content format,
- premise and hook hypothesis,
- why the reference is useful,
- requested outcome or CTA when stated,
- routing confidence,
- next worker and state.
The normalized fields never replace or alter the raw source.
# Workflow-gap rule
An object is allowed to exist before its production skill exists. If no registered writer or editor playbook matches the analyzed format:
1. Set Status to `NEEDS_PLAYBOOK`.
2. Leave Edit Skill empty.
3. Fill Required Workflow with the capability that is needed.
4. Fill Skill Gap with the missing skill, examples, inputs, outputs, and quality gates.
5. Keep the object visible in **00 — Workflow Gaps**.
Never route it through a merely similar skill. Building the missing playbook is a separate explicit task; the source and analysis remain preserved.
<page url="https://app.notion.com/p/3d099a426f9981f4b67fc0cfc5c874df">Human Guide — How to Use the Mansoor Content OS</page>
<page url="https://app.notion.com/p/3d099a426f998102b138c16bea752ff5">AI Implementation Contract — Mansoor Content OS</page>
<page url="https://app.notion.com/p/3d099a426f9981268a7adf409158f2d7">Build Prompt — Finish the Mansoor Content OS on Linux</page>
<database url="https://app.notion.com/p/3d099a426f99818a8de4ce1b41c7f4f2" inline="true" data-source-url="collection://b70abe56-526c-4189-85d4-8983e3e65966"></database>
<database url="https://app.notion.com/p/3d099a426f998181bc3ef5221ec56a77" inline="true" data-source-url="collection://b70abe56-526c-4189-85d4-8983e3e65966"></database>
<database url="https://app.notion.com/p/3d099a426f9981c4ba37f1e90fcc129f" inline="true" data-source-url="collection://b70abe56-526c-4189-85d4-8983e3e65966"></database>
<database url="https://app.notion.com/p/3d099a426f9981ea8e85d61857f70515" inline="true" data-source-url="collection://33c6a192-c09e-40f6-a450-92ca05c77511"></database>
</content>
</page>
