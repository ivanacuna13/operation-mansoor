---
name: mansoor-sales-call-clips
description: Edit unscripted Mansoor client sales-call footage into polished vertical reels that preserve a complete conflict-to-payoff arc, prefer sales-value beats (objection handling / upsell / presentation) when selecting cuts, distinguish the phone speaker with exact crop states, protect client identity, use approved opening and concluding headlines, pass deterministic QC, and deliver through Frame.io. Use for Mansoor calls, approval calls, client-win calls, or phone-reaction reels; use mansoor-talking-head-scripted-reels instead when a literal approved script controls the read.
---

# Mansoor Sales Call Clips

Treat the latest user instruction and timestamped review note as highest authority. Keep every raw source unchanged. This workflow is for unscripted calls: the verified recording and manually corrected transcript are spoken-content truth.

## Required routing

1. Read the project `AGENTS.md` and existing review state before touching the edit.
2. Use `hyperframes` first, then its routed `general-video`, `hyperframes-core`, `hyperframes-animation`, `hyperframes-audio`, and `hyperframes-cli` instructions for the composition and render.
3. Use `frameio-review-loop` for comments, revisions, and delivery. Never invent an uploader or return an unverified internal link.
4. Read all five task references before editing:
   - [Editorial workflow](references/editorial-workflow.md)
   - [Approved visual specification](references/visual-spec.md)
   - [QC and delivery gates](references/qc-delivery.md)
   - [Observed revision history and failure shields](references/revision-history.md)
   - [Frame-sourced edit rules (SC04/05/06)](references/frame-sourced-edit-rules.md)

## Lock the contract before editing

Create a project-local `sales-call-spec.json` from [the approved profile](references/approved-iul-profile.json). Record the exact source, premise, output limits, headline profile, client-speaker intervals, privacy events, Frame.io destination, and any explicitly approved deviation. Do not silently loosen a value to make validation pass.

The approved profile is mandatory for footage matching the seated close phone-call framing used in the IUL reel. If the source composition materially differs, calibrate only the subject-dependent crop origin and headline `top` value from still frames. Preserve every other invariant. Save the calibrated values in the project spec and visually prove them at the required snapshot times before rendering.


## Mansoor packaging doctrine (selection / story priority)

**Primary archive (file-sourced — not task text alone):**
- `references/sales-call-feedback-2026-09-04/` → `/home/box/mansoor-content-operations/context/mansoor/sales-call-feedback/`
- `2026-09-04-mansoor-imessage-upsell-feedback.md`
- `2026-09-04-mansoor-imessage-upsell-feedback.png`

This is **selection and packaging doctrine**, not Frame timestamp notes. Do not invent Frame comments from this section. Quote/summarize only what is in the archive files above.

From the archived Mansoor iMessage (edited) + Ivan follow-up:

- Great editing; good as **proof** that customers want it and that **“the calls are not hard.”**
- **“But the sales value is little.”** Need more **“objecting handling”** or **sales presentation**.
- Stated sales value: **“how to upsell existing policy holders on more valuable policies.”**
- Lesson (archive wording):
  1. They already have a policy. No problem
  2. Do you know how upsell?
  3. Find the need. Build value
- Ivan hook suggestion: **“I already have a policy.”**
- Archive background scraps (context only): “…that already had policies or had one in the past”; “There are some more with more conflict.”

**Soft-defaults (CM — keep one skill; do not invent beyond archive + these defaults):**
- When Mansoor/Ivan names an upsell (or objection/presentation) beat for the job, soft-default a **packaging priority** toward that beat over thin proof-only cuts. Still one skill — do not split into a separate upsell skill unless Ivan asks.
- If the assigned brief is pure good-news/eligibility proof and the recording has no upsell or objection beat, keep the truthful proof arc — do not fabricate sales dialogue.
- Still obey Frame-sourced visual/edit rules below. Packaging doctrine guides **which moment** to cut; Frame dumps govern **how** it looks and cuts.

## Build in four gates

### 1. Source and story gate

- Probe the exact source and create a word-timed transcript with speaker labels.
- Locate every client-name mention before cutting.
- Apply the Mansoor packaging doctrine when choosing among candidate arcs: prefer objection handling, sales presentation, or policyholder-upsell beats over thin proof-only moments when the recording contains them.
- Select the shortest complete arc: immediate setup / conflict, Mansoor handles the turn (good news, objection reply, or upsell), the real client reaction, only the explanation needed to understand the result, and an explicit resolution after the emotional or practical climax. Never end mid-conversation or before the payoff merely because the first reaction or peak objection beat occurred.
- After spoken content resolves, hold a **concluding resolution headline** stating the point in one short sentence. **Soft-default duration: ~7 seconds** (SC05 Frame exemplar). Frame SC04 also allows a 5–10 s band; treat SC06’s approved ~1.867–1.9 s closing card as an **approve-path outlier**, not the default (Ivan may override later — do not block waiting). Record text/timing in `sales-call-spec.json` as `resolution_headline` or `resolution_card`. Only use a non-default hold when the project `approved_deviations` documents it.
- Remove setup activity, non-talking footage, repeated words, filler, flubs, false starts, and avoidable silence. Preserve complete reactions and complete first/final phonemes. Every join must be free of flashing, lagging, blank, or half-second leftover frames.
- Save a speaker-aware edit map with source and output ranges. Picture-lock dialogue before styling.

### 2. Privacy and caption gate

- Fully mute each spoken client name from consonant onset through release and cover the same interval with one consistent, level bleep SFX. The name must not remain audible under the SFX.
- Caption from the verified final audio, not uncorrected ASR. Keep the real wording, spelling, financial terms, filler that remains audible, and reaction intact. Never summarize or paraphrase audible speech. Segment into one-line cards of at most five spoken words; target four or five, with shorter cards allowed only for a natural sentence ending or brief response.
- Mark phone speech with the approved yellow `CLIENT` pill and yellow caption. Mansoor captions remain white.

### 3. Visual gate

- Use a 1080×1920 canvas.
- Apply the approved headline, caption, and camera geometry from `visual-spec.md`; do not improvise a nearby layout.
- The opening headline is visible on the first rendered frame, stationary, and never enters. It starts fading at 10.00 seconds, is fully gone by 10.35 seconds, and never returns. Never animate its position or scale. No frames may exist at the start without that headline.
- The opening must be moving source footage with **Mansoor centered** in frame. Do not freeze the first frame, insert a still-image hold, open on off-center / away-from-subject footage, or allow blank frames before the headline unless the user explicitly approves that treatment.
- Every continuous client-speaking interval receives exactly one stable phone close-up beginning at the first client phoneme and ending at the first following Mansoor phoneme. Keep the close-up across pauses inside the same client turn (cut the pause; do not bounce crop). Reset to the normal crop immediately when Mansoor resumes. Never crop so tightly that captions are cut off.
- When a client crop overlaps the opening-headline window, protect Mansoor’s eyes by shifting the camera image, not the headline.
- After dialogue ends, show the concluding resolution headline/card per `visual-spec.md` and the project spec (**soft-default ~7 s**; SC04 5–10 s band; SC06 ~1.9 s only if approved_deviations).

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

A note about one instance of excessive whitespace, headline placement, crop timing, clipped speech, silence, caption error, identity leakage, flashing/lagging frames, off-center opening, missing concluding headline, or thin proof-only packaging when a stronger sales beat exists identifies a class of failure. Fix the noted timestamp, audit the entire reel for the same class, rerun the complete gate, and preserve prior comments and versions. Do not present a checker result as visual approval. Do not invent Frame comments that are not on disk.

## Completion statement

Report completion only after all automated and manual gates pass. State the final runtime, file size, public Frame link, transcode/public-viewer verification, and any deliberately approved deviation from the profile.
