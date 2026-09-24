---
name: Mansoor Drive sweeper
description: >-
  Grok dispatcher + Codex (Luna xhigh) worker for Mansoor Drive intake. When a
  Slack “upload complete” ping lands in MVP Agency #content-team, Grok filters
  and launches the sweeper wrapper; Codex identifies footage, renames, moves
  the package, and replies in the trigger thread. Do not use for Lifestyle
  Copycat cuts, talking-head clipping, or Drive polling.
---
# Mansoor Drive sweeper

Task bot job. Eddie is the face. This is Google Drive intake for Mansoor, not clipping and not Lifestyle Copycat cuts.

Grok is dispatcher only (see DISPATCHER vs CODEX above). Codex on Luna xhigh does identify/rename/move/reply.

Slack is the trigger. Drive is the files. Notion is not part of this job. Do not poll Drive on a timer.

## DISPATCHER vs CODEX (Luna xhigh) — LOCKED 2026-09-04

**Ivan correction LOCKED:**
- **Grok G Drive Sweeper bot** = always-on VM listener for Slack `#content-team` upload-complete pings. It does NOT poll Drive. It is the wake path only.
- **Codex `gpt-5.6-luna` `xhigh`** = only runs AFTER the ping, to identify footage+transcript, rename, MOVE, Slack reply. Codex is NOT watching for uploads / not an always-on inbox watcher.


| Role | Who | What |
| --- | --- | --- |
| **Dispatcher (Grok)** | G Drive Sweeper agent | Filter Slack event → `:white_check_mark:` via **copycat-cutter** → write packet → `python3 /home/box/mansoor-content-operations/tools/drive-sweeper/sweeper.py submit --packet-file …` → stay quiet on normal run; tell Eddie only on real blocker |
| **Worker (Codex)** | `gpt-5.6-luna` + reasoning `xhigh` | Identify from footage + transcript, rename, MOVE Drive files, Slack receipt as copycat-cutter |

**Grok must NOT** watch/download/inspect footage, rename, or move Drive files. Only: filter → reaction ack → call wrapper → report blocker/result.

Wrapper: `/home/box/mansoor-content-operations/tools/drive-sweeper/sweeper.py`
Codex skill: `/home/box/.codex/skills/mansoor-drive-sweeper/SKILL.md`
Config: `/home/box/mansoor-content-operations/config/drive-sweeper.json` (forces Luna/xhigh even if `system.json` is sol/high for other workers)

## Load every job

- This skill.
- Processed-state file at `/workspace/mansoor-sweeper/state.json` (create if missing).
- Confirm Composio connections before any mutation:
  - Slack `mansoor-slack` — MVP Agency, team `T0BQLF8P4AY`
  - Slackbot `copycat-cutter` — replies only, never Ivan
  - Google Drive `mansoor-drive` — Ivan Acuna `ivanacuna13@gmail.com`, must see Mansoor folders
- If any of those are not ACTIVE, stop. Fail-closed Slack reply. Do not move files.

## Locked IDs (verified 2026-09-03)

Workspace: MVP Agency `T0BQLF8P4AY`

| Who | Slack ID | Handle |
| --- | --- | --- |
| Ivan Acuna | `U0BQJP0DEGH` | `@ivanacuna13` |
| Mansoor Alzayer | `U0BQGPXNWCA` | `@instapire` |
| Composio app | `U0BQGU4FVU5` | `@composio` |

Channel: `#content-team` `C0BQKM27F5F`

Drive:

- Upload inbox: `1YKEGX9LH2Vt1akvVmCII2lUVKBUtfzGa` — https://drive.google.com/drive/folders/1YKEGX9LH2Vt1akvVmCII2lUVKBUtfzGa
- Mansoor Content root: `1fm-_1-mzNS8xfTDtv4Jq_92JX3QqJoQG` — https://drive.google.com/drive/folders/1fm-_1-mzNS8xfTDtv4Jq_92JX3QqJoQG
- Existing editor B-roll library (shortcuts; originals stay): `1OtoWJAihGH2a5Q38g8gLbHOkkldT1XOb` — https://drive.google.com/drive/folders/1OtoWJAihGH2a5Q38g8gLbHOkkldT1XOb

## Trigger filter (all must be true)

A wake is valid only when:

1. Newly created channel message (not an edit, not a reaction, not a thread reply that is not itself the trigger, not an old replay).
2. Channel is `C0BQKM27F5F`.
3. Sender is Ivan `U0BQJP0DEGH` or Mansoor `U0BQGPXNWCA`. Nobody else. No bots.
4. Message mentions Composio (`<@U0BQGU4FVU5>` or `@composio`).
5. Text contains `upload complete` case-insensitively. Extra words are fine (`new upload complete`).
6. This Slack message `ts` is not already in `state.json`.

If any check fails: do nothing. No Slack reply. No Drive reads required. Log the skip locally.

Never process the same Slack `ts` twice. After a handled event (success or fail-closed reply), append that `ts` to `state.json` before sending the result reply.

## Fired ack (first, before Drive)

The instant a trigger passes the filter, add a `:white_check_mark:` reaction on that Slack message via Composio `SLACKBOT_ADD_REACTION_TO_AN_ITEM` account `copycat-cutter`:

- channel: `C0BQKM27F5F`
- timestamp: the trigger `ts`
- name: `white_check_mark`

That is how Ivan knows it fired. Do this before listing Drive. Do not skip it. Do not post an “on it” text reply. The later thread reply is still the result.

If a new trigger arrives while a Drive job is already running: still add the green check immediately, then wait to file until the current job finishes. Do not start a second move pass on the same inbox.

## Auth window

A valid Ivan/Mansoor trigger authorizes inspect, identify, rename, and **move** of **this batch only**.

Never: delete, trash, publish, post to Notion, cut video, touch Lifestyle Copycat Slack, or touch files that are not in this batch.

## Batch ID

1. List the upload inbox. Paginate until complete.
2. Build the candidate set from Drive `createdTime` / `modifiedTime`, the Slack `ts`, and already-processed Drive file IDs in `state.json`.
3. Never assume every inbox file belongs to this upload. Leftovers from a prior fail-closed run stay until they can be identified as this package or a later trigger.
4. Wait until files are fully uploaded (size stable, not Google “still uploading”, no `incomplete` / zero-byte media).
5. Keep related files together: cameras, external audio, scripts. Do not split a package across destinations.
6. If the batch is uncertain, still uploading, or mixed with unrelated leftovers you cannot separate: leave the **entire** package in the inbox. Fail-closed reply. Do not guess.

Save processed Drive file IDs in `state.json` only after a successful move.

## Identify from footage + transcript, never filenames (LOCKED)

**Hard rule (Ivan):** never identify by filename. Upload inbox names are meaningless. Sweeper names and organizes **only after** inspecting footage and transcript (or equivalent spoken content / waveform evidence).

Banned shortcuts (fail closed if you were about to use any of these as the type/ID decision):
- Filename keywords (`sales`, `call`, `recruit`, `script`, `broll`, camera roll codes, DJI/IMG prefixes, etc.)
- Guessing type because a destination folder looks empty (including **Sales Calls** folder emptiness)
- Matching inbox name strings to an existing Drive folder name
- Routing from Slack text alone without media evidence

Required identify path:
1. Inspect the actual media (watch/listen or frame + audio evidence).
2. Use transcript / spoken content when available to confirm type and call/video name.
3. Pair external audio by timestamps, duration, scratch track, spoken content, and waveform — not by filename.
4. Only then choose type + destination + rename.

A scripted recruiting talking-head is still **Scripted Talking Heads**, not Recruiting Call.

Types:

- Scripted reel / scripted talking-head
- Sales call
- Recruiting call
- Lifestyle copycat B-roll package (raw for later remakes — do not cut)
- Live training
- Long-form YouTube
- Reusable B-roll

Hard routing rules:

- Month = month **filmed**, not month uploaded. Read media timestamps / capture date.
- Never put raw footage in Ready to Post or Uploaded Reels.
- Create only missing folders. Never duplicate a folder that already exists. Look up by ID, not name alone.
- Destination folder paths (including `Sales Calls`) are **after** type is proven from media — never use an empty Sales Calls folder as evidence that new inbox files are sales calls.
- Reusable B-roll goes into the existing `broll library` subject folder that already matches. Do not invent a parallel library. Do not move originals out of a place that editors already shortcut from unless this batch is clearly new inbox footage.
- Mansoor’s wife’s face must never be treated as Copycat-ready B-roll of her. File it, do not cut it here.
- Ski-lookalike in maroon quilted puffer, black LANGE helmet, GoPro, snow on the beard is Mansoor’s **dad**, not Mansoor.

If type or dest is uncertain after media+transcript inspection: leave the whole package in the inbox.

## Destinations (under Mansoor Content unless noted)

Month folder is `[Month YYYY]`, e.g. `August 2026`.

- Scripted reel → `[Month YYYY]/Scripted Talking Heads/[Video Name]/`
- Sales call → `[Month YYYY]/Sales Calls/[Call Name]/`
- Recruiting call → `[Month YYYY]/Recruiting Calls/[Call Name]/`
- Lifestyle copycat → `[Month YYYY]/Lifestyle Copycat Reels/[Video Name]/`
- Live training → `[Month YYYY]/Live Trainings/[Training Name]/`
- Long-form YT → `YouTube/[Project or Series Name]/`
- Reusable B-roll → `broll library/[best existing subject]/`

If type or dest is uncertain: leave the whole package in the inbox.

## Rename after ID, then move

Rename in Drive, then move. Preserve Drive file IDs. **Move, do not copy.**

- `[Video Name] - Raw.ext`
- `[Video Name] - External Audio.ext`
- `[Video Name] - Camera B.ext` / `Camera C`
- `[Video Name] - Script.ext`

Use Composio Drive `mansoor-drive`:

- List/find: `GOOGLEDRIVE_FIND_FILE` (folder_id + query) or native Drive `search_files` with `parentId = '…'`
- Create missing folder: `GOOGLEDRIVE_CREATE_FOLDER` with parent_id. Only if lookup shows it does not exist.
- Rename: native `update_file` `title`, or Composio equivalent.
- Move: `GOOGLEDRIVE_MOVE_FILE` with **both** `add_parents` (dest) and `remove_parents` (inbox `1YKEGX9LH2Vt1akvVmCII2lUVKBUtfzGa`). Omitting `remove_parents` leaves a second parent. That is not a move.
- `supports_all_drives`: true.

Never `trash_file`. Never copy.

## Fail-closed

Uncertain batch, type, audio pairing, dest, or still-uploading: leave the entire package in the inbox. Never guess dest. Never mark uncertain as success.

## Slack reply

Reply in the **trigger thread** (`thread_ts` = the trigger message `ts`). Channel `C0BQKM27F5F`.

Use Composio `SLACKBOT_SEND_MESSAGE` account `copycat-cutter`. Never `user-Slack` (that posts as Ivan). Never @Ivan. Never @Mansoor. Never `reply_broadcast`.

Success:

```
Upload processed
Type: …
Files: …
Drive: …
Needs identification: …
```

Omit `Needs identification` unless something still needs a human. Drive line is the dest folder URL.

Failure:

```
Upload not processed
Reason: …
No files were moved.
```

One reply per trigger `ts`. Check `state.json` for `replied_ts` before sending. Duplicate replies are a hard fail.

After a successful move: verify dest folder exists, names match, file IDs unchanged, package still together, then save state, then reply.

## Not this job

- Do not poll Drive.
- Do not cut, caption, or Slack a Lifestyle Copycat FILE. That is Copycat Cutter, and it posts to `#lifestyle-copycats` (`C0BQTR6RP97`), never `#content-team`.
- Do not clip talking-heads. That is Mansoor clipper.
- Do not ping Ivan in the Eddie chat for a normal processed upload. Slack thread is the receipt.
- Ping Eddie only if a connection is dead or the cold test is blocked.

## State file

`/workspace/mansoor-sweeper/state.json`

```json
{
  "processed_slack_ts": [],
  "replied_ts": [],
  "processed_drive_ids": [],
  "mansoor_slack_id": "U0BQGPXNWCA",
  "composio_slack_id": "U0BQGU4FVU5",
  "ivan_slack_id": "U0BQJP0DEGH"
}
```

## Done

Trigger matched, green check on the Slack message, batch identified, files renamed and moved (not copied), dest verified, state saved, one thread reply, no duplicate, no unrelated files touched.

## Clipping pipeline handoff (Sales / Genius / podcast)

When the batch is a **sales call**, **Genius call**, or podcast/clip source (not a scripted talking-head film upload):

1. Keep the raw recording as a **Content Source** only (never invent scripting/filming statuses).
2. Organize + rename in Drive, then attach folder/transcript links to the Source.
3. Run clip-selection → 0..N timestamped clips.
4. Create **one Content Object per clip** linked to that Source, Pipeline=`Clipping`, Status=`Ready to Edit`, with exact edit skill (`mansoor-sales-call-clips` or `mansoor-genius-clips`).
5. ZERO-CLIP: mark Source reviewed, create **0** Content Objects, **no Slack** status spam.
6. MULTI: one Source, N independent objects.
7. Before Ready to Edit validate: source, start, end, speaking arc, content type, exact edit skill, assigned editor, source relation — else BLOCKED with Blocked Reason / What Is Needed / Who Can Resolve It / Date Blocked / Previous State.
8. NEVER put Clipping objects in: Approved Ideas, Ready to Script, Script Needs Review, Script Revisions Needed, Ready to Film, Uploaded.

Scripted talking-head uploads still match to Ready to Film → Uploaded → Ready to Edit via Content PM `match-footage`.

