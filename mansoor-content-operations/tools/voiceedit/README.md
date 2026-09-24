# VoiceEdit Tools

Use these shared tools instead of writing per-episode render scripts.

## Main Command

For normal episode work, use `voiceedit_episode.py`. It creates or updates the
episode config/map, audits, renders a quiet proxy, writes QC, and can render the
final. If `transcripts/` is empty, it uses ElevenLabs Speech-to-Text directly
with the local `ELEVENLABS_API_KEY`; it must not call Jarvis MCP voice tools.

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_episode.py all \
  --episode /path/to/episode \
  --format hybrid_hosts_guest \
  --guest "Guest Name"
```

Use `--format remote_three_person` for fully remote episodes.

To prevent API transcription and require local transcripts:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_episode.py all \
  --episode /path/to/episode \
  --format hybrid_hosts_guest \
  --guest "Guest Name" \
  --no-transcribe
```

Render final only after the proxy is approved:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_episode.py final \
  --episode /path/to/episode
```

## Render Heartbeat

Every `proxy`, `final`, and `all` render writes a heartbeat file:

- proxy: `output/proxy_render_heartbeat.json`
- final: `output/final_render_heartbeat.json`

It includes ETA, progress, expected output size, actual output size, temp render
size, free storage, storage safety, output path, and log path.

Check status without tailing ffmpeg logs:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_episode.py status \
  --episode /path/to/episode \
  --mode proxy
```

Use heartbeat status instead of repeated manual "still rendering" polling.

## Audio Cleanup

Use `elevenlabs_audio_cleanup.py` for speech cleanup. This replaces the manual
Adobe Podcast loop for normal podcast work: extract audio, clean it with the
ElevenLabs Audio Isolation API, mux the cleaned audio back into the video, then
QC and upload the review artifact to Frame.io.

Clean a video in one command:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/elevenlabs_audio_cleanup.py clean-media \
  --video /path/to/PROXY_REVIEW_episode.mp4 \
  --output /path/to/PROXY_REVIEW_episode_clean_audio.mp4
```

Clean an audio file only:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/elevenlabs_audio_cleanup.py isolate \
  --source /path/to/program_audio.m4a \
  --output /path/to/program_audio.elevenlabs_isolated.m4a
```

Mux a cleaned audio file back into a video:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/elevenlabs_audio_cleanup.py mux \
  --video /path/to/PROXY_REVIEW_episode.mp4 \
  --audio /path/to/program_audio.elevenlabs_isolated.m4a \
  --output /path/to/PROXY_REVIEW_episode_clean_audio.mp4
```

The tool writes JSON state when `--state` is supplied and includes source/output
duration, file size, elapsed processing time, and duration drift after muxing.
It reads `ELEVENLABS_API_KEY` from the environment only.
Do not use Adobe Podcast browser
automation unless Ivan explicitly asks for Adobe Podcast or the ElevenLabs API
is unavailable.

## Final Delivery After Proxy Approval

Once Ivan approves the proxy, use `voiceedit_deliver_final.py` as the
deterministic final-delivery workflow. It can render the final, clean final
audio with ElevenLabs Audio Isolation, mux the cleaned audio back into the final,
upload the result to Frame.io, and print/save the public `share_url`.

For an existing final MP4:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_deliver_final.py \
  --episode /path/to/episode \
  --input-final /path/to/FINAL_episode.mp4 \
  --account-id FRAMEIO_ACCOUNT_ID \
  --folder-id FRAMEIO_FOLDER_ID \
  --project-id FRAMEIO_PROJECT_ID
```

For Tuned Talks, use the preset:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_deliver_final.py \
  --episode /path/to/episode \
  --input-final /path/to/FINAL_episode.mp4 \
  --frameio-preset tuned
```

To render final first, then clean/upload:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/voiceedit_deliver_final.py \
  --episode /path/to/episode \
  --render-final \
  --frameio-preset tuned
```

The delivery state is saved at `output/final_delivery/final_delivery.json` by
default. Return the `frameio_share_url` from the command output.

## Episode Types

- Hybrid hosts + remote guest:
  `render_hybrid_hosts_guest.py`
- Remote three-person:
  `render_remote_three_person.py`
- Single in-person 4K wide shot with virtual crops:
  `render_single_wide_virtual_multicam.py`

Use `single_wide_virtual_multicam` for Jim Norman / Flip Flippen style episodes:
one wide source, optional separate synced/cleaned program audio, and visual
switches made by cropping that single wide shot. This format keeps audio locked
to `program` and renders through one FFmpeg filtergraph to avoid per-segment AAC
drift.

## Required Per-Episode Files

- `episode_config.yaml`
- `base_cut_map.json`

These files hold episode-specific sources, crops, audio rules, and edit
decisions. The renderer code should stay shared.

## Audit

Run this before render:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/audit_base_cut.py \
  --config /path/to/episode_config.yaml \
  --map /path/to/base_cut_map.json \
  --report /path/to/output/base_cut_audit.json
```

## Hybrid Render

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/render_hybrid_hosts_guest.py \
  --config /path/to/episode_config.yaml \
  --map /path/to/base_cut_map.json \
  --output output/PROXY_REVIEW_episode.mp4 \
  --quiet \
  --log output/render.log
```

## Remote Render

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/render_remote_three_person.py \
  --config /path/to/episode_config.yaml \
  --map /path/to/base_cut_map.json \
  --output output/PROXY_REVIEW_episode.mp4 \
  --quiet \
  --log output/render.log
```

## Render Chatter Rule

Long renders must use `--quiet --log output/render.log --heartbeat
output/render_heartbeat.json`. Do not post repeated "still rendering" updates.
Report start with ETA/expected size/storage from the heartbeat, then completion
or failure. If status is needed, read the heartbeat file instead of tailing the
render log.

## Frame.io Review Bridge

Use `frameio_review.py` whenever Ivan wants timestamped review comments inside
Frame.io instead of QuickTime timestamp back-and-forth. This is not just for
proxies. Use it for base cuts, proxies, finals, QC clips, clip candidates, and
any other exported review file.

This tool uses the Frame.io API directly. It can use either a manually supplied
`FRAMEIO_ACCESS_TOKEN` or the cached Adobe OAuth Web App token at
`~/.codex/frameio_oauth.json`; it must not use Jarvis MCP tools. The local cache
is already set up on Ivan's machine and includes a refresh token.

Start by checking cached auth without printing secrets:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py oauth-status
```

Check the token:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py check-auth
```

If auth must be recreated, use OAuth Web App auth with no `email` scope:

```bash
FRAMEIO_CLIENT_SECRET="..." \
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py oauth-web-login \
  --client-id "ADOBE_WEB_APP_CLIENT_ID" \
  --redirect-uri "https://localhost:8765/callback" \
  --scope "openid profile offline_access additional_info.roles" \
  --store-client-secret
```

Important: the bridge must send a real `User-Agent` header. Frame.io may return
a bare HTML `403 Forbidden` when requests omit it. Do not remove the
`USER_AGENT` handling in `frameio_review.py`, and do not create one-off upload
scripts that skip it.

Find the account, workspace, project, and folder ids:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py list-accounts

python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py list-workspaces \
  --account-id FRAMEIO_ACCOUNT_ID

python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py list-projects \
  --account-id FRAMEIO_ACCOUNT_ID \
  --workspace-id FRAMEIO_WORKSPACE_ID

python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py list-children \
  --account-id FRAMEIO_ACCOUNT_ID \
  --folder-id FRAMEIO_PROJECT_ROOT_FOLDER_ID
```

Known Tuned Talks destination:

- account id: `2f141414-f1c3-4ee6-8cb8-4d8788946c0a`
- workspace id: `671e9161-9e7d-4fdc-886a-4d45049c4f70`
- project id: `e79a170a-ec84-48e3-a8bd-1308e3a0f4be`
- project root folder id: `ab36d3b6-1cf3-4404-aaed-d6c33f2644a9`

Upload any review file:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py upload-review \
  --episode /path/to/episode \
  --account-id FRAMEIO_ACCOUNT_ID \
  --folder-id FRAMEIO_FOLDER_ID \
  --project-id FRAMEIO_PROJECT_ID \
  --file /path/to/review-file.mp4 \
  --kind base_cut
```

Use `--kind proxy`, `--kind final`, `--kind qc`, or `--kind clip` as appropriate.
There is also a convenience wrapper for the newest `output/PROXY_REVIEW*.mp4`:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py upload-proxy \
  --episode /path/to/episode \
  --account-id FRAMEIO_ACCOUNT_ID \
  --folder-id FRAMEIO_FOLDER_ID \
  --project-id FRAMEIO_PROJECT_ID
```

Uploads write review-specific state under `output/frameio_reviews/`, plus a
latest pointer at `output/frameio_review.json`.
When `--project-id` is supplied, uploads also create a public commentable
Frame.io Share and print/save `share_url`. Give Ivan `share_url`, not the
internal `view_url`, because `share_url` is the clean review page for comments.

If a review file was uploaded before a share was created:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py create-share \
  --episode /path/to/episode \
  --kind base_cut \
  --project-id FRAMEIO_PROJECT_ID
```

After review comments are added in Frame.io, fetch them back into the episode:

```bash
python3 /Users/ivanclawd/Operation Mansoor/mansoor-content-operations/tools/voiceedit/frameio_review.py fetch-comments \
  --episode /path/to/episode \
  --kind base_cut
```

The fetched review becomes:

- `output/frameio_reviews/<kind>.comments.json`
- `output/frameio_reviews/<kind>.comments.md`

The comments are normalized to review-file timecode and mapped to the matching
`base_cut_map.json` segment when possible.

Start with polling via `fetch-comments`. Webhooks can be added later, but they
require an OAuth-backed Frame.io app and a public HTTPS receiver.
