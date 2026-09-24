https://app.notion.com/p/3be99a426f998142b4cdec87ea25707f?pvs=204

Here is the result of "fetch" for the Page with URL https://app.notion.com/p/3be99a426f998142b4cdec87ea25707f as of 2026-09-03T06:56:47.524Z:
<page url="https://app.notion.com/p/3be99a426f998142b4cdec87ea25707f" icon="🤖">
<ancestor-path>
<parent-page url="https://app.notion.com/p/e2799a426f99820c8244016564d6b29b" title=""/>
<ancestor-2-page url="https://app.notion.com/p/22199a426f9983f5b35a81ec692d770f" title=""/>
<ancestor-3-page url="https://app.notion.com/p/3be99a426f9981a8a423c2b66e0bf965" title="Operation Mansoor"/>
</ancestor-path>
<properties>
{"title":"Workers and Automations"}
</properties>

<content>
<callout icon="⚠️" color="yellow_bg">
	**Current reality:** The content model and Slack capture channel now exist. The Linux Drive Sweeper and Master Video Editor exist separately. The Mansoor Content PM, Idea Analyzer, and First Draft Writer are fully specified but remain **Prepared** until Grok Bot builds and activates their event listeners and Codex dispatchers.
</callout>
# What works today
## 1. Manual footage ingest
**Purpose:** Take one completed recording from Drive and organize it for production.
**How it starts:** Mansoor uploads the file to **upload here**. Someone sends Ivan the Drive link. Ivan asks Codex to process it.
**What Codex does:**
1. Confirms the upload is complete and the file opens.
2. Checks that it has not already been processed.
3. Preserves the original.
4. Extracts the audio.
5. Transcribes with ElevenLabs. Parakeet is the only fallback. Whisper is never used.
6. Identifies the date, content type, topic, and multipart order.
7. Renames the file using `MSR_YYYY-MM-DD_CONTENT-TYPE_TOPIC_v01.ext`.
8. Moves it into the correct month and folder.
9. Creates the required YouTube and Short Clip work in Notion.
10. Reports what was created.
**If it fails:** Stop at the failed step, preserve the original, and report the exact problem. Do not restart the entire workflow blindly.
**Status:** Manual and usable now.
# What is not active yet
## 2. Sandcastles idea research
**Purpose:** Add qualified Lifestyle Copycat ideas to **Ideas for Review**.
**When it can work:** After Sandcastles access and its MCP are connected.
**What it will do:**
1. Find relevant outlier videos.
2. Study the hook, structure, font, footage, song, pacing, and why the video worked.
3. Reject ideas that require false claims or another creator's identity.
4. Add the qualified idea to Notion with its source link and analysis.
5. Leave it for Ivan to approve.
**What it cannot do:** Approve its own idea, assign an editor before approval, or publish.
**Status:** Blocked until Sandcastles is connected.
## 3. Editor assignment
**Purpose:** Choose between Daoud and Nurmagomedov without using a permanent default.
**How the decision works:**
1. Check which editor is available.
2. Check how many active items each editor has in Notion.
3. Check their due dates.
4. Assign the editor with the lighter workload.
5. If the workload is equal, either editor is acceptable.
**Status:** Ready once both editors have assignable Notion identities.
# Editor delivery
After technical QC, the editor uploads the file into the correct shared Mansoor Drive folder and posts:
```javascript
TYPE: Lifestyle Copycat | Short Clip
PLATFORM: [destination platform]
FILE: [shared Google Drive file link]
```
Then the editor moves the Notion item to **Ready for Review**. Review comments go on the Drive file.
# Publishing
Publishing is manual and approval-gated.
1. The item reaches Ready to Post.
2. Confirm the approved final file and metadata.
3. Schedule through Post Bridge when supported.
4. Verify that it actually scheduled or posted.
5. Only then mark it Posted or Scheduled / Posted.
# Quick status
<table fit-page-width="true" header-row="true">
<tr>
<td>Process</td>
<td>Status</td>
<td>What is missing</td>
</tr>
<tr>
<td>Footage ingest</td>
<td>Manual and usable</td>
<td>Nothing required</td>
</tr>
<tr>
<td>Sandcastles research</td>
<td>Blocked</td>
<td>Sandcastles MCP connection</td>
</tr>
<tr>
<td>Editor assignment</td>
<td>Prepared</td>
<td>Assignable Daoud and Nurmagomedov identities</td>
</tr>
<tr>
<td>Review</td>
<td>Manual and usable</td>
<td>Nothing required</td>
</tr>
<tr>
<td>Publishing</td>
<td>Manual and usable</td>
<td>Approval and platform confirmation</td>
</tr>
</table>
# Mansoor Content OS control plane — 2026-09-03
- [Control Plane](https://app.notion.com/p/3d099a426f998109b014d2e3fc4b0e01)
- [Content Sources](https://app.notion.com/p/527c4746637e4cff9c4dc06c59ce255d)
- [Content Objects](https://app.notion.com/p/8439d827f39b4c47acd9e17271045038)
- [Shoot Batches](https://app.notion.com/p/a36b0d0b40ec49a787d4df63ab90ef40)
- Slack capture: private **#content-ideas-inbox** (`C0BU7H12J4F`)
After activation, every eligible root message creates a source/content object. Scripted Talking Heads automatically proceed through analysis and first-draft writing. Future formats are analyzed and stop at `IDEA_REVIEW` until Ivan approves them. Editing begins only after footage is matched and the object reaches `READY_TO_EDIT`, at which point the existing Master Video Editor dispatcher receives the validated job packet.
</content>
</page>
