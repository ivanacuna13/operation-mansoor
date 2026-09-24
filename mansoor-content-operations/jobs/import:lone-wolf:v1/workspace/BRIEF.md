# Mansoor - The Lone Wolf

- workflow: general-video
- flow: autonomous
- format: Instagram Reel, 1080x1920
- source: precision picture lock using the external DJI microphone
- headline: Being the best closer / is keeping you stuck
- captions: exact spoken wording, Inter Bold, sentence case, -0.08em tracking, subtle settle
- treatment: lower highlights, mild contrast and saturation, deeper blacks, restrained crop-ins
- music: Hans Zimmer - Time; non-hip-hop and phone-audible under dialogue

# STEER — LIVE REVISION (Ivan lock NOW)

Before you Slack or set Edit Ready for Review:
1. Read MVE_REVISION_FAILCLOSED_GATE.md
2. Produce qc/frame-comment-checklist.json with EVERY unresolved Frame comment → timestamp → fixed=yes|no + proof
3. Audit whole cut for same mistake classes
4. Run: python3 /home/box/mansoor-content-operations/tools/master-video-editor/mve.py delivery-gate --job-id <this job>
5. Gate must return ok=true. Else DO NOT Slack; stay Edit Revisions Needed.

Wrapper will also fail-closed on exit without a passing checklist.

