# QC and delivery gates

## Pre-render evidence

Save deterministic snapshots in the project. At minimum include:

- headline: the exact first rendered frame, 0.30, 9.90, 10.20, 10.50, and 11.20 seconds;
- opening center: first rendered frame must show Mansoor centered with moving footage;
- every edit join ±0.5 seconds for flashing/lagging leftover frames;
- concluding resolution headline/card: first frame, midpoint, and last frame of the hold;
- midpoint and last two frames of every client-speaking interval;
- first two frames after every client interval;
- every name-bleep interval;
- both sides of every jump cut;
- first and final spoken frames.

Inspect at native 1080×1920 and at phone size. A layout checker cannot judge the forehead gap, empty white space, whether a phone is obvious, or whether a crop feels like the wrong speaker.

## Picture and dialogue lock

- The arc reaches the good news and genuine reaction quickly.
- There is no non-talking setup footage, false start, repeated word, flub, or off-premise section.
- No avoidable pause remains at a join; inspect any seam near or above 0.12 s.
- Every first and final phoneme is complete.
- The complete client reaction and any phrase necessary to understand it remain, followed by an explicit conversational resolution rather than a mid-call cutoff.
- When Mansoor/Ivan names an upsell/objection/presentation beat, or the recording contains those beats, confirm the cut packages that sales-value lesson rather than a thin proof-only moment (Mansoor packaging doctrine; archive under `references/sales-call-feedback-2026-09-04/`). Soft-default packaging priority; keep one skill.
- A concluding resolution headline/card holds **~7 seconds** by soft-default (SC05), within the SC04 5–10 s band, with one short sentence stating the point. SC06 ~1.867–1.9 s is an approve-path outlier — only via project `approved_deviations`.
- No flashing, lagging, blank, or black leftover frames at joins.
- A fresh final-audio transcript has been compared with the manually corrected transcript.
- Every join passes waveform, listening, and boundary-frame inspection.

## Privacy and audio

- Every selected name occurrence is listed in the privacy map.
- Original name audio is zeroed for the full phoneme interval.
- One consistent bleep covers each interval without a level jump or exposed syllable.
- Client voice remains understandable on phone speakers.
- Full-program loudness and true peak are measured; no clipping is present.
- The file decodes from start to finish with FFmpeg.

## Headline and crop matrix

- 0.30 s: fixed headline, correct compact width and type, immediately above forehead.
- 9.90 s: still fully visible, same coordinates and scale as 0.30 s.
- 10.20 s: only opacity has changed.
- 10.50 s and every later sample: completely absent.
- Every client midpoint: stable phone close-up, phone obvious, facial identity anchor present, yellow `CLIENT` treatment visible.
- Every following Mansoor frame: normal crop restored.
- If the headline and a client close-up overlap, the image was shifted to protect the eye; headline geometry did not change.

## Captions

- Captions match the final audible wording character for character.
- Every card contains at most five spoken words and remains at the approved 68 px size; shorter cards occur only at natural endings or brief responses.
- Mansoor is white; client is yellow with `CLIENT` pill.
- No client name appears in text.
- No one-line caption wraps or overflows.
- Caption entrances settle quickly and remain seek-safe.
- Continuous speech does not contain an unexplained caption gap.
- Every caption and `CLIENT` pill is horizontally centered at the review frame, including the exact timestamps named in reviewer notes.
- During every client phone close-up midpoint, captions remain fully on-frame (not cropped by the zoom).

## Automated gate

Run from the skill directory or call the script by absolute path:

```bash
python3 scripts/qc_sales_call.py \
  --video /absolute/path/to/final.mp4 \
  --composition /absolute/path/to/index.html \
  --spec /absolute/path/to/sales-call-spec.json \
  --decode
```

The script checks the delivery file, exact profile geometry, headline behavior, and client-caption/crop coverage. Fix failures at their source. Do not edit the spec to excuse an unapproved render.

Before rendering, also require a normalized CFR H.264 picture lock with keyframes no farther than 1.10 seconds apart. A sparse-keyframe warning is a failed gate because it can cause freezes or missing extracted frames.

After it passes, generate a full-duration contact sheet with enough samples to show all crop states and visually inspect every tile. Save the QC output and contact sheet outside temporary render directories.

## File gate

- MP4 container with H.264 video and AAC audio.
- Exactly 1080×1920, square pixels, 9:16.
- Runtime strictly below 90.00 seconds.
- File size strictly below 150,000,000 bytes.
- Fast-start metadata preferred for mobile review.
- Final filename is clear and versioned.

## Frame.io gate

Use the existing review state and stable public share. For a revision:

1. Preserve prior review files and comments.
2. Upload a clearly versioned corrected asset to the intended folder and project.
3. Maintain the existing version context and share when it works. If the public viewer cannot display the stack, retain the internal stack and attach the newest standalone asset to the same public share.
4. Poll until the new file reports `transcoded`, not merely `uploaded`.
5. Confirm the public share contains the intended new file or head.
6. Request the public deep link, follow redirects, require HTTP 200, and confirm the returned page identifies the exact new filename.
7. Return the public review link. Do not return only an internal project URL.

Do not claim a Frame.io repair is complete because upload succeeded. The public viewer itself must be verified.

## MVP Agency Slack handoff gate

Apply this section only when the user requests Slack delivery. The verified public Frame.io link is the canonical review link.

### Message and sequencing contract

- Post each video as its own top-level message in the requested MVP Agency channel. Send one message, verify it, then send the next. Never batch or multi-execute the posts.
- Resolve Ivan's Slack user ID in the target workspace and use exactly this four-line body, substituting only that verified user ID and the verified Frame.io public link:

  ```text
  <@IVAN_USER_ID>
  TYPE: Mansoor Sales Call Clip
  PLATFORM: Instagram
  FILE: <verified Frame.io public link>
  ```

- Do not call the asset top-, middle-, or bottom-of-funnel. Funnel stage is not the content type.
- Do not add a greeting, `Hi Mansoor`, a Mansoor tag, the video title, premise, date, status prose, or any other text to the message body.
- Put the descriptive video name in the uploaded filename, not in the Slack message body.

### Sender and tagging guardrail

1. Read back the connected Slack account identity and workspace before posting.
2. Use the approved MVP Agency Composio Slackbot connection and its bot/service identity for the delivery. Do not post from Ivan's personal Slack identity.
3. Never self-tag the authenticated sender. Tag Ivan from the verified bot identity; never tag Mansoor.
4. If the required bot identity is unavailable, stop and report the blocker. Do not fall back to Ivan's account, impersonate a bot, or send an incorrect post.
5. After every post, read back the exact channel, sender, root-message body, and link before advancing to the next asset.

### Review reactions

Ivan reacts directly to the bot-authored root delivery message:

- ✅ — approved and good to go.
- 📝 — Frame.io notes were left. Read the notes, revise the same asset/version stack, rerun every QC gate, and return the verified revision link.
- ❌ — rejected. Stop work on that asset and await replacement direction.

Apply the reaction only to the asset delivered by that exact root message. Silence is not approval.
