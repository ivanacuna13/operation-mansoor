# MVE REVISION FAIL-CLOSED GATE (LOCKED 2026-09-07 — Ivan)

BEFORE any Slack revise delivery / Notion **Edit Ready for Review**:

1. Fetch ALL unresolved Frame.io comments for this asset
2. Map each to an edit timestamp
3. Apply each correction
4. Write checklist: `qc/frame-comment-checklist.json` with every comment id/text → timestamp → fixed=yes|no + proof note
5. Audit the ENTIRE video for the same mistake class as each comment
6. Run: `python3 /home/box/mansoor-content-operations/tools/master-video-editor/mve.py delivery-gate --job-id <JOB_ID>`
7. Only if EVERY row is `fixed=yes` AND `unresolved_frame_comments_remaining=0` → upload new Frame version stack head, ONE Composio copycat-cutter reply, register reply ts, Notion Edit Ready for Review
8. If any row is `fixed=no` OR any unresolved comment remains → DO NOT post Slack; stay **Edit Revisions Needed**; leave the open checklist on disk for CM

No Grok editing. No "mostly done." Fail closed.
