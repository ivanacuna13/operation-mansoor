# Pending Linux owner install

The corrected sales-call skill is staged at:

`/home/box/mansoor-content-operations/review/mansoor-sales-call-skill-update/mansoor-sales-call-clips/`

The installed target is owner-protected from `codex-review`. Run as Linux user `box`:

```bash
cp -a /home/box/.codex/skills/mansoor-sales-call-clips /home/box/.codex/skills/mansoor-sales-call-clips.before-2026-09-03-review-fix
rsync -a --delete /home/box/mansoor-content-operations/review/mansoor-sales-call-skill-update/mansoor-sales-call-clips/ /home/box/.codex/skills/mansoor-sales-call-clips/
python3 -m py_compile /home/box/.codex/skills/mansoor-sales-call-clips/scripts/qc_sales_call.py
```

Expected SHA-256:

- `SKILL.md`: `dab5b3085f380de5882ac2b0bdd232fb53efd3521d8d126b8bc159fd94f7b504`
- `scripts/qc_sales_call.py`: `9e4215d3e16f4a0e9899197631f480e65cbd1e7f1a4cdbe693cc214ce4b48eae`

