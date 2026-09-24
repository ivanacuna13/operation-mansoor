---
name: mansoor-sales-call-clips
description: Edit unscripted Mansoor client sales-call footage into polished vertical reels that preserve the good-news/reaction arc, distinguish the phone speaker with exact crop states, protect client identity, use the approved headline and caption geometry, pass deterministic QC, and deliver through Frame.io. Use for Mansoor calls, approval calls, client-win calls, or phone-reaction reels; use mansoor-talking-head-scripted-reels instead when a literal approved script controls the read.
---

# Mansoor Sales Call Clips

Treat the latest user instruction and timestamped review note as highest authority. Keep every raw source unchanged. This workflow is for unscripted calls: the verified recording and manually corrected transcript are spoken-content truth.

## Required routing

1. Read the project `AGENTS.md` and existing review state before touching the edit.
2. Use `hyperframes` first, then its routed `general-video`, `hyperframes-core`, `hyperframes-animation`, `hyperframes-audio`, and `hyperframes-cli` instructions for the composition and render.
3. Use `frameio-review-loop` for comments, revisions, and delivery. Never invent an uploader or return an unverified internal link.
4. Read all four task references before editing:
   - [Editorial workflow](references/editorial-workflow.md)
   - [Approved visual specification](references/visual-spec.md)
   - [QC and delivery gates](references/qc-delivery.md)
   - [Observed revision history and failure shields](references/revision-history.md)

## Lock the contract before editing

Create a project-local `sales-call-spec.json` from [the approved profile](references/approved-iul-profile.json). Record the exact source, premise, output limits, headline profile, client-speaker intervals, privacy events, Frame.io destination, and any explicitly approved deviation. Do not silently loosen a value to make validation pass.

The approved profile is mandatory for footage matching the seated close phone-call framing used in the IUL reel. If the source composition materially differs, calibrate only the subject-dependent crop origin and headline `top` value from still frames. Preserve every other invariant. Save the calibrated values in the project spec and visually prove them at the required snapshot times before rendering.

## Build in four gates

### 1. Source and story gate

- Probe the exact source and create a word-timed transcript with speaker labels.
- Locate every client-name mention before cutting.
- Select the shortest complete arc: immediate setup, Mansoor delivers the good news, the real client reaction, only the explanation needed to understand the result, and an explicit resolution after the emotional or practical climax. Never end mid-conversation merely because the first reaction occurred.
- Remove setup activity, non-talking footage, repeated words, filler, flubs, false starts, and avoidable silence. Preserve complete reactions and complete first/final phonemes.
- Save a speaker-aware edit map with source and output ranges. Picture-lock dialogue before styling.

### 2. Privacy and caption gate

- Fully mute each spoken client name from consonant onset through release and cover the same interval with one consistent, level bleep SFX. The name must not remain audible under the SFX.
- Caption from the verified final audio, not uncorrected ASR. Keep the real wording, spelling, financial terms, filler that remains audible, and reaction intact. Never summarize or paraphrase audible speech. Segment into one-line cards of at most five spoken words; target four or five, with shorter cards allowed only for a natural sentence ending or brief response.
- Mark phone speech with the approved yellow `CLIENT` pill and yellow caption. Mansoor captions remain white.

### 3. Visual gate

- Use a 1080×1920 canvas.
- Apply the approved headline, caption, and camera geometry from `visual-spec.md`; do not improvise a nearby layout.
- The headline is visible on the first rendered frame, stationary, and never enters. It starts fading at 10.00 seconds, is fully gone by 10.35 seconds, and never returns. Never animate its position or scale.
- The opening must be moving source footage. Do not freeze the first frame, insert a still-image hold, or allow blank frames before the headline unless the user explicitly approves that treatment.
- Every continuous client-speaking interval receives exactly one stable phone close-up beginning at the first client phoneme and ending at the first following Mansoor phoneme. Reset to the normal crop immediately afterward.
- When a client crop overlaps the headline window, protect Mansoor’s eyes by shifting the camera image, not the headline.

### 4. Render and delivery gate

- Normalize every picture lock to CFR H.264 with a maximum one-second keyframe interval (`-r 30 -g 30 -keyint_min 30 -sc_threshold 0`) before HyperFrames rendering. Sparse-keyframe warnings reopen media prep; they are not harmless.
- Run HyperFrames check and the project snapshots before the final render.
- Run `scripts/qc_sales_call.py` against the composition, project spec, and rendered MP4. A nonzero exit reopens the edit.
- Independently inspect the actual export, the full contact sheet, every client crop boundary, headline frames at 9.90/10.20/10.50 seconds, all bleep windows, and every dialogue join.
- Deliver only an H.264/AAC 1080×1920 MP4 under 90 seconds and under 150 MB.
- Upload the corrected version into the existing Frame.io review context. Wait for `transcoded`, verify the intended head/file, and confirm the public viewer returns HTTP 200 and identifies the new filename.
- If Slack handoff is requested, follow the exact one-asset-at-a-time protocol in `references/qc-delivery.md`. A funnel stage is never the content `TYPE`; for this workflow the fixed type is `Mansoor Sales Call Clip`.
- Deliver through the approved MVP Agency Composio Slackbot connection. Ivan reviews by reacting directly to the bot-authored delivery message with ✅, 📝, or ❌; follow the matching action in `references/qc-delivery.md`.

## Revision rule

A note about one instance of excessive whitespace, headline placement, crop timing, clipped speech, silence, caption error, or identity leakage identifies a class of failure. Fix the noted timestamp, audit the entire reel for the same class, rerun the complete gate, and preserve prior comments and versions. Do not present a checker result as visual approval.

## Completion statement

Report completion only after all automated and manual gates pass. State the final runtime, file size, public Frame link, transcode/public-viewer verification, and any deliberately approved deviation from the profile.
