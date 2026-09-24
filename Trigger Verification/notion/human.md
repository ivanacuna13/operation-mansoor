https://app.notion.com/p/3d099a426f9981f4b67fc0cfc5c874df?pvs=204

Here is the result of "fetch" for the Page with URL https://app.notion.com/p/3d099a426f9981f4b67fc0cfc5c874df as of 2026-09-03T07:04:35.570Z:
<page url="https://app.notion.com/p/3d099a426f9981f4b67fc0cfc5c874df" icon="👋">
<ancestor-path>
<parent-page url="https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01" title="Mansoor Content OS — Control Plane"/>
<ancestor-2-page url="https://app.notion.com/p/3be99a426f9981a8a423c2b66e0bf965" title="Operation Mansoor"/>
</ancestor-path>
<properties>
{"title":"Human Guide — How to Use the Mansoor Content OS"}
</properties>

<content>
<callout icon="👋" color="green_bg">
	**Use this page tomorrow:** it explains the system without implementation details.
</callout>
# The basic idea
Every publishable Mansoor video is its own **Content Object**. A reference video, voice note, sales call, or rough thought is a **Source**. One source can create one or many videos.
You no longer need to make a dated Google Doc with several script tabs, manually title every idea, copy links between tools, or remember which footage belongs to which script.
# Where things go
- **Ideas:** private Slack channel **#content-ideas-inbox**
- **Scripts and status:** <mention-page url="https://app.notion.com/p/8439d827f39b4c47acd9e17271045038"/>
- **Raw references and recordings:** <mention-page url="https://app.notion.com/p/527c4746637e4cff9c4dc06c59ce255d"/>
- **What Mansoor should film:** the **03 — Ready to Film** view in Content Objects
- **Filming groups:** <mention-page url="https://app.notion.com/p/a36b0d0b40ec49a787d4df63ab90ef40"/>
- **Footage:** Google Drive
- **Video review:** [Frame.io](http://Frame.io), delivered through **#content-team**
# Sending an idea
Drop the idea into **#content-ideas-inbox** exactly as you have it:
- share an Instagram or YouTube link,
- upload a screenshot or reference video,
- send a voice note,
- write a rough thought,
- add a sentence explaining what you like.
You do not need a title or template.
Optional labels can force routing:
- `[talking-head]`
- `[sales-skit]`
- `[roleplay]`
- `[tofu-copycat]`
- `[sales-call]`
- `[genius]`
# What happens to a talking-head idea
1. The PM preserves the raw Slack message.
2. It creates one Source and one Content Object.
3. The Analyzer extracts the transcript, hook, structure, and transferable idea.
4. The Writer creates a first draft inside that Content Object.
5. You receive `Your draft is ready to review: [Notion link]` in the original Slack thread.
6. ✅ means ready to film.
7. 📝 means use the notes in that thread or on the Notion page and revise the same Codex writing session.
8. ❌ archives the idea.
# What happens to a skit, roleplay, or TOFU copycat
1. It is still captured and analyzed.
2. It stops at `IDEA_REVIEW`.
3. You receive `I analyzed this idea. Approve it if you want me to write the draft: [Notion link]`.
4. ✅ approves the idea for its format-specific writing workflow.
5. 📝 requests changes to the analysis using your thread or Notion notes.
6. ❌ archives it.
If the correct writer or editor skill does not exist, it moves to `NEEDS_PLAYBOOK`. The missing workflow is shown in **00 — Workflow Gaps**. The system must not improvise with the wrong skill.
# Filming
Approved scripts move to `READY_TO_FILM`. Mansoor only needs the filtered Ready to Film view. Shoot Batches can group several scripts, but every script remains its own Content Object.
# After Mansoor uploads
The Drive Sweeper organizes uploads and emits a structured completion event. The PM matches the organized footage and any external microphone audio to the right Content Object. Uncertain matches stay visible for review.
Once a complete object reaches `READY_TO_EDIT`, the PM sends a validated JSON packet to the existing Master Video Editor. That dispatcher launches the correct Codex editing skill and stores the session ID.
# Video review
The editor performs QC, uploads to [Frame.io](http://Frame.io), and delivers one video per top-level message in **#content-team**.
- ✅ approved
- 📝 [Frame.io](http://Frame.io) notes exist; resume the original Codex editor session, apply them, QC, and upload a new version in the same stack
- ❌ rejected
# What exists now
- Slack channel and instructions: **built**
- Notion Sources, Content Objects, Shoot Batches, views, and playbook records: **built**
- Master Video Editor dispatcher on Linux: **built and cold-tested**
- Drive Sweeper: **already exists**
- Content PM, Idea Analyzer, and First Draft Writer Grok bots: **fully specified; still need to be built and activated on Linux**
# Rule for future changes
Add new formats to the same object system. Create or approve a matching writer/editor playbook before dispatch. Do not create a second tracker, a second intake channel, or a separate document system.
# Slack should stay simple
Slack messages will explain only what happened, what you should do, and where to click. Technical states and bot details stay in Notion. You should never need to understand the automation to use the channel.
</content>
</page>
