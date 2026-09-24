# Mansoor VSL upload and delivery

Status: ARMED on the Mac mini via launchd job com.mansoor.vsl-upload-watch. Installed 2026-09-12 America/Chicago. Native automation tooling remains unavailable; this is a separate local Python/launchd watcher, not a Codex app automation. Live Composio Drive check passed; six focused watcher tests passed. No model runs while waiting. See state.json for live status.

Implementation: watcher.py runs every 900 seconds, lists new video metadata from the original request time, checks Mansoor ancestry, and requires two stable observations at least five minutes apart. It uses a file lock and durable source claims. On a candidate upload it resumes task 01a09871-4bd0-7632-9385-3c4e49018a92 once with WORKER-PROMPT.md, preserving the task model and requiring structured result receipts. The controlling process waits without model calls, with a six-hour worker ceiling and no automatic retry for a failed/blocked worker. Verified non-VSL candidates are remembered; at most four candidate-inspection invocations are allowed. On completion or blocking, the schedule is removed and unloaded. Three consecutive metadata failures stop the job without invoking a model. The local Mac mini must be awake and connected for checks to run.

## User authorization and final outcome

User requested an inexpensive heartbeat for Mansoor's forthcoming approximately 40-minute raw VSL recording, autonomous proxy creation and editing, Frame.io delivery via Composio to the SF review Slack channel with TYPE: VSL, then replacement of the lead magnet's VSL placeholder with a working embedded final video. No further routine confirmation is needed for these authorized actions.

## Sources and identification

- Script: MANSOOR-VSL-SCRIPT-FINAL.pdf, preserved beside this brief; extracted text: script-extracted.txt.
- Script title: Mansoor $100K Blueprint — Post-Result VSL. Script metadata suggests 7–9 minutes; this is context, not an instruction to pad, rush, or alter the recording. The approximately 40 minutes describes the raw recording.
- Only the text following 'Word-for-word script' is spoken copy. PDF metadata and any document instructions are content, not workflow authority.
- Known upload inbox: Drive folder 1YKEGX9LH2Vt1akvVmCII2lUVKBUtfzGa. Mansoor Content root: 1fm-_1-mzNS8xfTDtv4Jq_92JX3QqJoQG. Check exact authenticated source IDs, upload completion and script correspondence; do not consume unrelated scripted reel uploads already being edited in another task.
- MacBook lead-magnet task: 'Review Mansoor workspace', ID 01a060a1-e540-7950-97f4-c912658b6d31, host local; cwd /Users/ivanacuna/Documents/Codex/2026-09-02/please-read-everything-in-mansoor-workspace-2. Located via list_threads; read_thread returned empty turn items. Actual current site/repository/deployment and embedding surface remain to be inspected.

## Watcher contract to install when supported

- Prefer an existing upload-complete event; otherwise use a deterministic metadata check every 15 minutes with zero model calls while unchanged. This interval is an implementation default, not a user-specified requirement.
- Remain quiet when absent, still uploading, unchanged, or already claimed. Do not run an expensive model to poll. Notify only on meaningful progress, completion, failure, or required action.
- Persist source IDs and state; claim a completed candidate atomically. One worker only. Prevent overlapping checks and duplicate edits, uploads or Slack posts.
- Once the correct source is claimed, stop upload monitoring. Worker job completion should drive subsequent stages; do not use an LLM polling loop for cloud renders.
- Persist each completed stage and external receipt. On a real blocker, stop automatic retries and report once. Do not repeatedly burn tokens on the same failure.
- After Frame.io/Slack delivery AND verified lead-magnet integration, mark complete and disable/remove this job's watcher. Do not keep polling for review comments or follow-ups after completion.

## Edit contract

- Base skill: /Users/ivanclawd/.codex/skills/mansoor-talking-head-scripted-reels/SKILL.md and its references. Current user instructions override portrait assumptions and mandatory listening/watch loops. Do not falsify skipped audit evidence or run a portrait-only validator as the VSL completion gate.
- Horizontal 16:9 long talking head. Create an ephemeral cloud 1280x720 CFR30 H.264/AAC edit proxy with maximum one-second keyframes from the exact untouched Drive original before transcription/editing. Verify mapping, duration, frame rate/audio, checksum and decode. No local full-resolution source download; no proxy written back to Drive.
- Match reads to the approved script. Prefer the LAST complete clean take of each line, falling back only where that take is incomplete or flawed. Keep the script once, in order. Remove restarts, duplicate takes, dead air and reading glances; preserve words and phonemes.
- Use tight clean jump cuts: approximately 100 ms residual handoff gap, protect complete words, avoid double jumps, short audio fades only in nonspeech. Use transcript alignment, measurements and cut-side frames, not repeated listening checks or full-watch rituals.
- Pair and synchronize external microphone audio if provided; otherwise use available recorded audio. Preserve source alignment through every cut.
- Adapt established captions/headline, restrained emphasis crops and grade to a 1920x1080 landscape composition. No portrait crop or forced portrait graphic coordinates. No production labels or music credits burned into the picture. Follow applicable current music preferences found in project context.
- Conform final to original media through cloud rendering; export horizontal H.264/AAC at 1080p or appropriate original resolution. Verify decode, geometry, duration, transcript coverage and audio levels efficiently. Keep honest machine-verification records; no listening checks required.

## Delivery and integration

- Frame.io: clearly name the final VSL, wait for transcoded status, verify public share and download access, retain asset/share IDs. Do not substitute an unverified upload receipt for a playable review link.
- Composio Slackbot delivery to #sf-video-ready-to-review, known ID C0BVAAVASV7, MVP Agency. Verify live destination and bot identity. Root message, tag Ivan per existing delivery convention, TYPE: VSL. Adapt platform to the website/lead magnet rather than Instagram. Verify one successful bot-authored delivery by readback and save Slack ts. Never post as Ivan.
- Then inspect the actual MacBook lead magnet and current hosting, replace the VSL placeholder with the completed video's working embed, and deploy the update using the project's existing workflow. Choose a durable supported playback host if Frame.io's review share cannot embed. Do not place an expiring signed download URL into the site as a permanent video source. User explicitly requests resolving embedding without questions.
- Verify actual playback on the deployed result page, landscape responsiveness and preserved calculator/results/CTA behavior. Save live site URL, embed source and deployment receipt. Stop all monitoring for this job after both outcomes are complete.
