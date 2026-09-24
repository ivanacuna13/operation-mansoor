---
workflow: general-video
flow: automation
storyboard: no
message: "A felony did not prevent this prospect from qualifying for an IUL"
destination: instagram-reels
aspect: 1080x1920
language: en
length: 52.800s
angle: real-sales-call-proof
---

## Intent

Turn an unscripted Mansoor client call into a concise vertical proof clip: Mansoor explains that a five-year underwriting lookback makes the prospect eligible, then the prospect confirms how the probation timeline works.

## Assets

- `.media/video/video_001.mp4` — baked dialogue-only picture lock with the reviewed residual interval removed.
- `.media/audio/voice/voice_001.wav` — matching separated dialogue, ending at the exact Frame.io note timestamp.
- `.media/images/image_001.png` — frozen source frame for the six-second resolution card.

## Customizations

- Fixed two-line premise card that fades away once at ten seconds.
- Yellow `CLIENT` captions and an immediate 1.25x phone crop only while the client speaks.
- A six-second closing resolution headline after the dialogue: “This is why you don’t give up on your clients.”

## Notes

- Preserve 9:16, stay under 90 seconds and 150 MB, use no music, and do not expose client names.
- Bleep the possible client name at 1.00–1.52 seconds and omit it from captions.

# STEER — LIVE REVISION (Ivan lock NOW)

Before you Slack or set Edit Ready for Review:
1. Read MVE_REVISION_FAILCLOSED_GATE.md
2. Produce qc/frame-comment-checklist.json with EVERY unresolved Frame comment → timestamp → fixed=yes|no + proof
3. Audit whole cut for same mistake classes
4. Run: python3 /home/box/mansoor-content-operations/tools/master-video-editor/mve.py delivery-gate --job-id <this job>
5. Gate must return ok=true. Else DO NOT Slack; stay Edit Revisions Needed.

Wrapper will also fail-closed on exit without a passing checklist.

