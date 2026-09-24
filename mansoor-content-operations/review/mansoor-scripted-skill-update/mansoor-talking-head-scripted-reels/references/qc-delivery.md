# Fail-closed QC and delivery

## Required audit file

The final validator requires one JSON audit. Start from the `boundary-audit.json` created by `scripts/build_boundary_audit.py`, then add the top-level sections below. Paths must point to durable evidence files.

```json
{
  "reel": "identified reel name",
  "opening": {
    "non_speech_seconds": 0.06,
    "first_word_intact": true,
    "direct_eye_contact": true,
    "no_setup_glance": true
  },
  "closing": {
    "non_speech_seconds": 0.10,
    "last_word_intact": true,
    "no_read_down": true
  },
  "boundaries": [],
  "transcript": {
    "fresh_picture_lock_transcript": "/absolute/path/transcript.json",
    "script_diff_zero": true,
    "quiet_word_tails_checked": true
  },
  "captions": {
    "full_resolution_reviewed": true,
    "phone_size_reviewed": true,
    "no_awkward_wraps": true,
    "no_face_overlap": true,
    "cta_keyword": "BLUEPRINT"
  },
  "headline": {
    "full_resolution_frame": "/absolute/path/headline-full.jpg",
    "phone_size_frame": "/absolute/path/headline-phone.jpg",
    "full_resolution_reviewed": true,
    "phone_size_reviewed": true,
    "sits_on_or_just_above_forehead": true,
    "not_high_in_empty_space": true,
    "clear_of_eyes_and_mouth": true,
    "all_overlapping_crop_states_checked": true,
    "hook_claim_accurate": true
  },
  "audio": {
    "external_mic_verified": true,
    "camera_scratch_muted": true,
    "sync_start_mid_end_verified": true,
    "music_track": "/absolute/path/music.ext",
    "non_hip_hop": true,
    "energetic_cinematic_fit": true,
    "phone_music_audible": true,
    "phone_speech_effortless": true,
    "dialogue_to_music_db": 17.0,
    "integrated_lufs": -14.2,
    "true_peak_dbfs": -1.5
  },
  "visual": {
    "early_middle_late_grade_checked": true,
    "skin_and_clothing_detail_preserved": true,
    "crop_beats_meaningful": true,
    "crop_safe_areas_checked": true,
    "contact_sheet": "/absolute/path/final-contact.jpg"
  },
  "batch": {
    "all_reels_checked_for_shared_failure_classes": true,
    "classes_checked": [
      "clipped words",
      "sentence pauses",
      "read-down tails",
      "caption equality",
      "headline size and placement",
      "crop emphasis",
      "music fit and level"
    ]
  }
}
```

Each boundary entry must have the generated `index`, `output_time`, `previous_last_word`, `next_first_word`, and `evidence_image`, plus:

```json
{
  "measured_nonspeech_seconds": 0.10,
  "outgoing_word_intact": true,
  "incoming_word_intact": true,
  "outgoing_direct_eye_contact": true,
  "incoming_direct_eye_contact": true,
  "no_retained_read_down": true,
  "no_visual_glitch_or_double_jump": true,
  "listened_normal_speed": true,
  "listened_eyes_closed": true,
  "cut_side_frames_inspected": true
}
```

Do not set a review field to true from an automated checker alone.

## Gates enforced by the validator

- The manifest contains ordered, contiguous script segments.
- Caption JSON equals the manifest wording exactly after whitespace normalization.
- Rendered DOM caption text equals caption JSON.
- Caption timings have no unexplained gap greater than one 30 fps frame.
- Caption cue boundaries are backed by fresh word timestamps; a proportional or evenly divided timing generator fails.
- Inter Bold, sentence case, `-0.08em` tracking, phone-readable caption size, and the headline minimum ratio are present.
- A quoted uppercase CTA keyword is present when specified.
- Every join has evidence and all manual review fields pass.
- Opening nonspeech is at most 80 ms; each internal gap is at most 160 ms; closing nonspeech is at most 150 ms.
- `scripts/measure_speech_gaps.py` reports no final-render sentence gap above 160 ms and no final-render voice silence above 180 ms at `-32 dB`, including pauses inside a sentence and internal boundaries within a source segment.
- The headline is visibly present and fully opaque in the actual 0.000-second frame; CSS or GSAP that begins it at opacity zero fails.
- The full-resolution and phone headline frames exist and all placement checks pass.
- External mic, sync, camera mute, non-hip-hop music, phone listening, grade, crop, and batch propagation checks pass.
- Integrated loudness is between -15 and -13 LUFS and true peak is no higher than -1 dBTP.
- FFprobe confirms a 1080x1920 portrait H.264 video with AAC 48 kHz stereo audio, and FFmpeg decodes the entire file.

## Independent final watch

After the validator passes, watch the actual final export once from beginning to end without stopping. Then review:

- the opening first word and headline;
- every jump cut and sentence handoff;
- every crop transition;
- a representative sample of caption lengths plus every number, name, brand term, and CTA;
- the final sentence and tail.

If anything looks or sounds wrong, the validator pass is stale: fix the edit, regenerate evidence, and rerun it.

## Frame.io delivery

For a new reel, upload a clearly named review asset and create a mobile public share. For a revision, add the corrected asset to the existing version stack and preserve the stable share and comments.

Before reporting a link:

1. Verify the uploaded asset is the newest stack head.
2. Wait for `transcoded`, not merely `uploaded`.
3. Confirm the public share points to the intended stack or asset.
4. Request the stable public link and verify HTTP 200.
5. If the viewer still fails, do not claim delivery. Repair the share relationship or provide a verified standalone fallback while retaining version history.

## MVP Agency Slack delivery

Apply this stage only when the user has authorized Slack delivery. It occurs after every local QC and Frame.io gate above has passed.

### Identity and destination gate

- Use the Composio **Slackbot** toolkit connection for the MVP Agency workspace. It must publish as the connected bot identity.
- Do not use a Composio `slack` connection authenticated as Ivan or any other human. A message sent through Ivan's human connection cannot meaningfully tag Ivan for review.
- Resolve `#content-team` to its live channel ID and resolve **Ivan Acuna** to exactly one live Slack member ID before writing. Do not reuse a guessed display-name mention.
- The returned sender must be a bot and must not equal Ivan's user ID. If it does, stop before the next reel and correct the connection.

### File and message contract

Name the Frame.io asset itself with the reel name before delivery:

```text
Mansoor - <Video Name> - Final v<number>.mp4
```

The Slack body must not repeat the video name. Post one reel at a time as its own root message, with no `thread_ts`. Wait for a successful response before sending the next reel. Use exactly this four-line body:

```text
<@IVAN_USER_ID>
TYPE: Scripted Talking Head
PLATFORM: Instagram
FILE: https://f.io/<public-share-id>
```

Do not add `Hi Mansoor`, tag Mansoor, add a greeting, add a date, name the reel in the body, or classify the reel as top, middle, or bottom funnel. `TYPE` is the production skill type: `Scripted Talking Head`.

### Delivery verification

After each message:

1. Confirm the write response reports success.
2. Confirm a bot identity authored the message and the sender ID differs from Ivan's tagged ID.
3. Confirm the body contains only the Ivan mention and the exact `TYPE`, `PLATFORM`, and `FILE` lines above.
4. Confirm the Frame.io unfurl or link points to the intended, correctly named, transcoded asset.

After the batch, fetch the latest `#content-team` history and verify every reel appears once as a separate bot-authored root message. Remove any superseded messages created during a failed delivery attempt when the posting identity has permission, then read back the channel again. Never report delivery from the send response alone.

Interpret review reactions on each delivery message as follows:

- check-mark emoji: approved and good to go;
- notes or memo emoji: comments were left on the Frame.io link and require review;
- X emoji: rejected entirely.
