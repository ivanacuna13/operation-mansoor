https://app.notion.com/p/3d099a426f998172a70bc24d6783917a?pvs=204

Here is the result of "fetch" for the Page with URL https://app.notion.com/p/3d099a426f998172a70bc24d6783917a as of 2026-09-03T07:03:53.293Z:
<page url="https://app.notion.com/p/3d099a426f998172a70bc24d6783917a" icon="🤖">
<ancestor-path>
<parent-page url="https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01" title="Mansoor Content OS — Control Plane"/>
<ancestor-2-page url="https://app.notion.com/p/3be99a426f9981a8a423c2b66e0bf965" title="Operation Mansoor"/>
</ancestor-path>
<properties>
{"title":"Build Prompt — Mansoor Content PM"}
</properties>

<content>
<callout icon="🤖" color="purple_bg">
	**Copy this entire page into Grok Bot. Build the bot; do not simulate the workflow.**
</callout>
# Build target
Create a delegation bot named **Mansoor Content PM** on the Linux machine. It is the control-plane dispatcher for content intake and state transitions. Eddie may remain the visible Grok persona. The bot itself must not analyze references, write scripts, edit video, transcribe media, upload assets, or publish.
# Existing environment
- Workspace: `/home/box/mansoor-content-operations`
- Codex CLI is authenticated and supports `gpt-5.6-sol` plus resume by session ID.
- Master Video Editor is ready at `/home/box/mansoor-content-operations/tools/master-video-editor/mve.py`.
- Its registry is `/home/box/mansoor-content-operations/state/master-video-editor.sqlite`.
- Slack workspace: MVP Agency.
- Private capture channel: `#content-ideas-inbox`, ID `C0BU7H12J4F`. The ID is the stable trigger even if the display name changes again.
- Delivery/review channel: `#content-team`, ID `C0BQKM27F5F`.
- Ivan Slack user ID: `U0BQJP0DEGH`.
- Notion Content Sources database: `527c4746637e4cff9c4dc06c59ce255d`, data source `33c6a192-c09e-40f6-a450-92ca05c77511`.
- Notion Content Objects database: `8439d827f39b4c47acd9e17271045038`, data source `b70abe56-526c-4189-85d4-8983e3e65966`.
- Notion Shoot Batches database: `a36b0d0b40ec49a787d4df63ab90ef40`, data source `8ae3a3d3-9be5-4f6f-b90c-cf18fbb74405`.
# Trigger
Subscribe to new root-message events in `C0BU7H12J4F`. Do not poll channel history. Ignore:
- messages from bots,
- message edits that have already been handled,
- thread replies unless they are explicit revision/control commands,
- duplicates with the same channel ID and timestamp.
Treat every eligible root message as committed content work. Scripted Talking Head ideas proceed automatically to a first draft. Other recognized formats are analyzed and held at `IDEA_REVIEW` until Ivan approves them.
# Intake transaction
For each eligible event:
1. Compute `event_key = slack:C0BU7H12J4F:{message_ts}`.
2. Lock that key in a local SQLite registry before external writes.
3. Preserve the original text, links, attachments, sender ID, channel ID, message timestamp, and Slack permalink.
4. Detect source type: Instagram Reference, Sandcastles, Sales Call, Genius Call, YouTube, Slack Note, or Other.
5. Generate a plain working title from the source or message. Do not require Ivan to name it.
6. Create exactly one Content Sources page with:
	- Source
	- Source Type
	- Source URL when present
	- Slack Channel ID = `C0BU7H12J4F`
	- Slack Message TS
	- Capture Date
	- Analysis Status = `Queued`
	- Notes containing any capture text not represented elsewhere
7. For an idea/reference/note, create exactly one related Content Object immediately:
	- Content = generated working title
	- Format = infer conservatively from the message/reference; default `Scripted Talking Head`. Supported idea formats include `Scripted Talking Head`, `Scripted Sales Call Skit`, and `TOFU Copycat`.
	- Status = `IDEA_CAPTURED`
	- Source = created Source page
	- Working Title
	- Edit Skill = `mansoor-talking-head-scripted-reels` for Scripted Talking Head
	- Platforms = Instagram and YouTube Shorts unless the message explicitly says otherwise
	- Priority = Normal
8. For Sales Call or Genius Call recordings, create the Source only. The analyzer may return zero or more clip candidates; create a separate Content Object for every accepted candidate.
9. Persist all Notion page IDs and URLs in SQLite.
10. Reply once in the Slack thread using plain English: `Got it — I saved this here: {content_object_url}`. For source-only captures say `Got it — I saved the source here: {source_url}`.
11. Launch the Mansoor Idea Analyzer through Codex. Store its Codex session ID and job ID.
# Automatic continuation
When analysis succeeds:
1. Validate the analyzer JSON contract.
2. Update the Source page body and set Analysis Status to `Analyzed`.
3. Update the existing Content Object with the hook, angle, and analysis summary.
4. If Format is `Scripted Talking Head`, set Status to `DRAFTING` and automatically launch the Mansoor First Draft Writer.
5. If Format is `Scripted Sales Call Skit`, `TOFU Copycat`, or another future idea format, set Status to `IDEA_REVIEW`. Do not launch writing until Ivan reacts ✅ to the PM's Slack thread message or explicitly approves in the thread. On approval, set `DRAFTING` and launch the format-specific writer. A 📝 reaction means resume the analyzer session with Ivan's notes; ❌ sets `ARCHIVED` and cancels downstream work.
6. For Sales Call/Genius sources, create only candidates that pass the analyzer's self-contained/value/truth gates, then route them toward editing with the correct source timestamp.
When writing succeeds:
1. Validate the writer JSON contract.
2. Update the Content Object page body with the full canonical script and its analysis/history sections.
3. Mirror the script to the Canonical Script property when it fits.
4. Set Draft Version and Status = `SCRIPT_REVIEW`.
5. Reply in the original Slack thread: `Your draft is ready to review: {content_object_url}`.
# Later production handoff
- `READY_TO_FILM` items appear in the existing Notion view for Mansoor.
- The PM may group selected items into Shoot Batches without copying scripts into separate Google Docs.
- When the Drive Sweeper emits a structured upload-complete event, match footage to Content Objects using script transcript, file metadata, capture/batch context, and confidence.
- Do not route uncertain matches. Set `FOOTAGE_MATCHING` and record the ambiguity.
- When all required footage/audio/script fields are present, set `READY_TO_EDIT` and submit the exact validated JSON job packet to the existing Master Video Editor wrapper. Never bypass it.
# Revision and review
Store the original Codex session ID for every analyzer, writer, and editor chain. Revisions resume the same session. Never spawn a fresh session for the same object's revision unless the prior session is irrecoverable and the replacement is explicitly logged.
# Required local implementation
Create:
- `/home/box/mansoor-content-operations/CONTENT_PM.md`
- `/home/box/mansoor-content-operations/config/content-pm.json`
- `/home/box/mansoor-content-operations/tools/content-pm/pm.py`
- `/home/box/mansoor-content-operations/state/content-pm.sqlite`
- fixtures and tests under `/home/box/mansoor-content-operations/tests/content-pm/`
SQLite must record events, sources, content objects, jobs, state transitions, attempts, errors, and Codex session IDs.
# Safety
- Idempotent at every boundary.
- Fail closed.
- Never invent a transcript, source claim, proof point, number, testimonial, or URL.
- Never perform media work inside Grok.
- Never create a second Notion content system.
- Never delete or migrate historical records during this build.
# Cold tests
Run without processing real footage:
1. Slack idea event creates one Source and one Content Object fixture.
2. Duplicate event creates nothing new.
3. Instagram link routes to analyzer.
4. Scripted Talking Head analyzer success routes automatically to writer; future formats stop at IDEA_REVIEW until Ivan approves.
5. Sales call analyzer can return zero or multiple content objects.
6. Failed Notion write remains retryable without duplicate creation.
7. READY_TO_EDIT produces a valid Master Video Editor packet.
8. Missing script for scripted talking head blocks dispatch.
9. Stored Codex session resumes for revision.
10. Grok refuses any request to edit or inspect footage directly.
Return a readiness report with created files, tests passed/failed, exact blockers, and one real but harmless Slack-to-Notion cold test using a test message only.
# Human submission contract
Do not require structured Slack messages. Accept a link, attachment, screenshot/video, voice note, rough sentence, or any combination. Preserve the raw event unchanged, then normalize it.
Optional labels override inference: `[talking-head]`, `[sales-skit]`, `[tofu-copycat]`, `[sales-call]`, and `[genius]`.
Generate and store: working title, source type, intended format, premise, hook hypothesis, why it may work, explicit CTA/outcome if present, routing confidence from 0 to 1, and next action.
During the current phase, an unlabeled idea/reference defaults to `Scripted Talking Head`. If confidence is below 0.65 and a wrong choice would materially change the workflow, ask exactly one short clarification in the Slack thread and set the object to `BLOCKED` with blocker `AWAITING_FORMAT_CLARIFICATION`. Resume the same event after the reply. Do not ask for information that can be inferred from the source.
# Skill-registry gate
Before moving any object beyond `IDEA_REVIEW`, resolve both a writer workflow and an editor skill from an explicit registry. Exact format compatibility is required. If either is missing:
- set Status = `NEEDS_PLAYBOOK`,
- leave Edit Skill empty when the editor skill is missing,
- populate Required Workflow,
- populate Skill Gap with the missing component and expected contract,
- notify in the original Slack thread: `I saved this, but we do not have instructions for making this type of video yet: {notion_url}`.
Do not fall back to `general-video` or a similar skill merely to keep the pipeline moving. Add a cold test proving an unknown roleplay format lands in NEEDS_PLAYBOOK and does not dispatch.
# Slack writing rule
All user-facing Slack copy must be easy English. Never say routing, object, dispatcher, workflow gap, state code, job ID, validator, idempotency, packet, stack trace, or internal error name. Translate every status into what happened and what the person should do next. Keep messages to one or two short sentences plus a link.
</content>
</page>
