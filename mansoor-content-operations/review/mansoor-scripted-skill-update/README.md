# Mansoor scripted reel skill update

Replace `/home/box/.codex/skills/mansoor-talking-head-scripted-reels/` with the contents of `mansoor-talking-head-scripted-reels/`, preserving ownership for user `box`. Then run:

```bash
python3 -m py_compile /home/box/.codex/skills/mansoor-talking-head-scripted-reels/scripts/*.py
```

This update fixes the September 2 QC failure: measure pauses from the actual rendered voice track, inspect sentence boundaries inside manifest segments, align canonical captions to post-lock word timestamps, require the headline at frame zero, and re-transcribe isolated boundary candidates when long-file timestamps drift.
