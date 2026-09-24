# Sales-call skill doctrine update — 2026-09-04

Builder-only documentation. No media edits. No Slack posts.

## What was updated

**Live install (authoritative):** `/home/box/.codex/skills/mansoor-sales-call-clips/`

**Writable review mirror of this pass:** `/home/box/mansoor-content-operations/review/mansoor-sales-call-skill-update-2026-09-04/mansoor-sales-call-clips/`

**Prior locked staging (codex-review owned, not writable by box):** `/home/box/mansoor-content-operations/review/mansoor-sales-call-skill-update/` — still contains the 2026-09-03 draft; do not treat as current.

**Backup of pre-update install:** `/home/box/.codex/skills/mansoor-sales-call-clips.before-2026-09-04-doctrine-update/`

Also mirrored under learning: `/home/box/mansoor-content-operations/learning/SALES_CALL_DOCTRINE_UPDATE_2026-09-04.md`

### Files touched in the skill

- `SKILL.md` — Mansoor packaging doctrine (labeled) + Frame-backed opening/ending/cut rules
- `references/frame-sourced-edit-rules.md` — **new**; quoted Frame extracts with paths
- `references/editorial-workflow.md`
- `references/visual-spec.md`
- `references/revision-history.md`
- `references/qc-delivery.md`
- `references/approved-iul-profile.json`

Also absorbed the earlier 2026-09-03 review staging improvements that had not been fully installed (first-frame headline, 68 px / ≤5-word captions, no still open, GOP media prep, Slack reaction protocol).

## Rules added (with sources)

### A) Mansoor packaging doctrine — NOT Frame timestamps

Source (file-sourced): `/home/box/mansoor-content-operations/context/mansoor/sales-call-feedback/2026-09-04-mansoor-imessage-upsell-feedback.md` + `.png`, linked from skill `references/sales-call-feedback-2026-09-04/`. Explicitly labeled in SKILL + editorial-workflow + profile JSON. Not task-text-only.

- Prefer “objecting handling” / sales presentation over thin proof-only value (archive wording)
- Theme: upsell existing policy holders on more valuable policies
- Lesson beat (archive): already have policy → do you know how upsell? → find the need → build value
- Hook suggestion (Ivan): “I already have a policy.”
- Soft-default packaging priority when Mansoor/Ivan names that beat; keep one skill

### B) Frame-sourced visual/edit rules — real dumps

Full extract: skill `references/frame-sourced-edit-rules.md`.

| Rule | Source path |
| --- | --- |
| No frames at start without headline | `jobs/import:sales-call-04-felony:v1/.../clip.comments.md` @00:00:00; same on SC06 clip |
| Moving open (no still) | `.../sales-call-05-twenty:.../clip.comments.md` @00:00:03.333 |
| Mansoor centered at open | `.../sales-call-05-twenty:.../revision_final.comments.md` @00:00:01.667 |
| Headline not too high/small | SC05/SC06 clip + SC06 revision_final |
| Captions 1 line / ~4–5 words; readable size | SC04/SC06 `clip.comments.md` |
| Captions centered; never cropped off by zoom | SC06 clip @00:00:22.167; revision_final @00:00:10.167 |
| Cut pauses; no flashing/lagging ~0.5s leftover frames | SC04/05/06 revision_final (+ SC04 clip glitchy cut) |
| Crop at first client phoneme; hold across in-turn pauses | SC04 `clip.comments.md` |
| Correct speaker attribution | SC04 clip; SC06 revision_final |
| Do not end before payoff/climax | SC04/SC06 clip |
| Concluding resolution headline ~5–10s (SC04) / ~7s exemplar (SC05) | SC04/05/06 `revision_final.comments.md`; verified SC04 `qc/revision-v5/QC-REPORT.md` (6.0s); SC05 `qc/v4-manual-qc.json` (7.0s) |

## What is still missing / needed from CM

1. ~~**iMessage primary dump on disk**~~ — **DONE 2026-09-04:** archived at `context/mansoor/sales-call-feedback/` and skill symlink `references/sales-call-feedback-2026-09-04/`; packaging doctrine is file-sourced.
2. **Slack revision-thread digests** — `slack-revision-reply.json` for SC04/05/06 only record `blocked_before_bot_send`; no Slack note digests with extra edit doctrine.
3. ~~**Standardize closing-card duration**~~ — **soft-default applied:** ~7s (SC05). SC06 ~1.867–1.9s = approve-path outlier. Ivan may override later; do not block waiting.
4. **Concluding-card visual treatment** — SC04 contextual card over still vs SC05 on-picture resolution headline. Need one approved profile.
5. **Learning ledger promotion** — `learning/RULES_LEARNED.md` / accepted-rules have no sales-call Frame promotions yet (only scripted-reel spelling fixtures).
6. ~~**Selection priority when briefs conflict**~~ — **soft-default applied:** packaging priority when Mansoor/Ivan names an upsell/objection/presentation beat; keep one skill until Ivan asks to split. Pure-proof briefs without that beat stay truthful.

## Explicitly not done

- No media re-edits
- No Slack posts / spam
- No invented Frame timestamps or fabricated reviewer quotes
