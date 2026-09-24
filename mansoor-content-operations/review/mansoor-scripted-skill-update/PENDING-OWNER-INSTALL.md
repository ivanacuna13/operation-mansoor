# Mansoor scripted reel skill update

The staged skill contains the September 3 QC repair. Install it as Linux user `box` only after preserving the current skill:

```bash
cp -a /home/box/.codex/skills/mansoor-talking-head-scripted-reels /home/box/.codex/skills/mansoor-talking-head-scripted-reels.before-2026-09-03-qc-fix
rsync -a --delete /home/box/mansoor-content-operations/review/mansoor-scripted-skill-update/mansoor-talking-head-scripted-reels/ /home/box/.codex/skills/mansoor-talking-head-scripted-reels/
python3 -m py_compile /home/box/.codex/skills/mansoor-talking-head-scripted-reels/scripts/*.py
```

Required behavioral change: measure exact picture-lock audio at -32 dB; fail any silence above 180 ms, including pauses inside one ASR sentence and one manifest segment. Do not let punctuation tokens or -40 dB room noise create a false pass.
