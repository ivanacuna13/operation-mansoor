# Mansoor Script Delivery (HYBRID — LOCKED)

Gold format reference (read-aloud shape Ivan approved):
`/home/box/mansoor-content-operations/context/mansoor/GOLD_SCRIPT_FORMAT_mansoor-scripts-9_1.txt`
(also `/workspace/mansoor-scripts-9_1.txt`)

Inspiration/source text can be longer. **OUTPUT** always uses the gold line format below.

> **LOCKED decision (Ivan):** hybrid model. Do **not** revert to “Script property only” or “body forever / optional Script mirror.”

## HYBRID model (authoritative)

| Phase | Source of truth | Who |
| --- | --- | --- |
| **During review** | Notion **page body** (gold: short title + one sentence per line) | Human (Ivan) — full-size editor. Do **not** make him use the tiny **Script** property. |
| **On Slack ✅ approve** (or Script Locked) | Content PM copies page-body script → Notion **Script** property, then Status → **Ready to Film** (+ Talent Mansoor) | Content PM |
| **After approve / MVE** | Locked **Script** property (populated at approve only) | Machines (MVE / downstream) |

Also:

- **`Script Locked`** checkbox = OK as extra lock signal (same film-queue path as ✅).
- **Notion page comments** = revision notes (preferred).
- **Slack emoji** = pickup / approve signal — **not** the notes and **not** a second SoT.

Do **not** use the name **Canonical Script** (Ivan rejects that label).
Do **not** invent a separate “line by line reading” section — the body *is* the gold script during review.

Internal JSON may still use key `canonical_script` / `script` — that value is what the first-draft writer emits and Content PM writes into the **page body** on `apply-draft`.

## Exact output format

```
short title
First spoken sentence on its own line.
Second spoken sentence on its own line.
Third spoken sentence on its own line.
…
DM me the word "LEVERAGE" and I'll send it to you.
```

Rules:

1. Line 1 = short title (working title / slug vibe). Not a paragraph.
2. Every spoken sentence = its **own** line. No fat paragraphs.
3. Optional blank lines between beats for breath/pacing are OK (gold file does this on some pieces). Still never pack multiple sentences into one dense paragraph block.
4. `filming_lines` = the spoken lines only (title excluded), same order, complete sentences Mansoor can film.
5. `script` / `canonical_script` = title + newline + those lines joined with `\n` (same text that lands in the Notion **page body** at draft delivery).
6. Keyword CTA = CAPITALS inside quotes, e.g. `"LEVERAGE"` / `"BLUEPRINT"`.

## Exact ✅ / approve flow

1. First-draft writer emits gold-format JSON (`script` / `canonical_script`).
2. Content PM `apply-draft` writes that text into the Notion **page body**, clears/empties property **Script**, sets **`Script Locked`=false**, Status = **Script Needs Review** (lean props only).
3. Ivan opens the Content Object and edits the **page body** until it reads right. Notes go in **Notion comments** (not Slack).
4. Ivan reacts **✅** (approve-as-is) or **🧠** (edited body + learn) on the Slack delivery message (or checks **Script Locked**).
5. Content PM `reaction(approve)` → `sync_script_lock` (✅). `reaction(learn_approve)` / emoji `brain` → body diff + learning ledger → then `sync_script_lock`:
   - **Extract** gold script from page body (strip delivery footer / italic instructions; stop at divider).
   - **Set** property **`Script`** = that body text.
   - **Set** **`Script Locked`=true**, Status → **Ready to Film**, Talent = Mansoor (Film Next).
6. MVE / downstream read the locked **Script** property (not the body).

Do **not** clobber Ivan’s Notion body edit with an older bot draft once he has edited / locked it.

## How body script is parsed

Helpers in `tools/content-os/notion_actions.py`:

- `read_page_body_script(page)` — prefers `children` → `children_to_plain_script`, else `body_markdown` → `extract_script_from_body_markdown`.
- Stops before `---` divider and italic footer lines (`_Edit…`, `_When…`, `_On approve…`, `_Notes…`).
- `resolve_script_for_approve(page, packet, extras)` — body first (human SoT on approve), then legacy Script / extras (old cards).
- `write_script_property(text)` — required on approve: flat props for machine **Script** (+ Script Locked).
- `resolve_script_for_machine(page, extras, status)` — after Ready to Film / Ready to Edit: prefer **Script** property, fallback body.

## Revision notes

- Preferred: Notion page comments → `pm.py apply-notion-comment` → Status **Script Revisions Needed**, resume the **same** writer Codex session, overwrite **page body**, clear **Script Locked**, Status back to **Script Needs Review**.
- Slack 📝 is a pickup ping that still requires a Notion note (or thread note) before resume.

## Slack emoji meanings

| Signal | Meaning |
| --- | --- |
| ✅ | **Approve** → body → Script → Ready to Film |
| 📝 | Pickup: revision notes exist (look at Notion comments) |
| ❌ | **BLOCKED** |
| Notion **`Script Locked`** | Same film-queue path as ✅ (extra signal) |
| Slack **🧠** / `brain` on script-ready | Diff body vs prior draft → learn into `mansoor-first-draft-writer` ledger → then same film lock as ✅; clarifying Qs + voice-note feedback in thread (`learn-script-feedback`) |
| Notion **page body** | Human SoT during review |
| Notion **Script** property | Machine SoT after approve only |

## New vs old cards

- **New** Script Needs Review cards: gold script in **page body**; Script property empty until approve; `Script Locked` checkbox available.
- **Old** cards that still put the only copy in property `Script` / Canonical Script: Content Manager migrates when touching them (copy into page body for review, or on approve ensure Script is populated). Builder does not unblock or re-dispatch live cards.

## Who owns what

- **Builder / Idea Guy / first-draft writer:** emit gold format; write **page body** via Content PM; no Slack spam; no live unblock.
- **Content Manager / Content PM:** on ✅ / Script Locked, copy body → Script, film queue, Talent, old-card migration; Notion comments for revisions.


## Slack delivery routing (LOCKED)
- `#content-ideas-inbox` `C0BU7H12J4F` = intake only
- `#ai-content-team` `C0BV0Q7JZ6H` = ALL bot deliverables (scripts + videos)
- `#content-team` `C0BQKM27F5F` = human content team (do not dump AI deliverables)

### Script ready Slack shape (top-level in #ai-content-team)
```
New Script ready for review
Type: Scripted Talking Head / Sales Call Roleplay / …
Reference: (link)
Script: (link)
```

- **Bulk post lock:** one Slack message per Content Object in `#ai-content-team`. Never combine multiple scripts/videos into one large message.


## #ai-content-team delivery shapes (LOCKED)
Scripts (top-level, one message per item):
```
New Script ready for review
Type: …
Reference: <original Instagram/source video URL — NEVER Notion>
Script: <Notion content page URL>
```
Videos (top-level, one message per item, **no Script line**):
- Sales Call Clip: `TYPE` + `PLATFORM` + `Headline:` (on-screen text, not Title) + `FILE`
- Scripted Talking Head: `TYPE: Scripted Talking Head` + `PLATFORM` + `Headline:` + `FILE`

## GOLD BODY ONLY (LOCKED 2026-09-04)
Notion page body for Script Needs Review = short title + one sentence per line ONLY.
FORBIDDEN in page body: Hook, Angle, Why it may work, Premise blocks, Canonical Script label, analysis sections, instruction footers.
Hook/Angle/Why may live in Notion *properties* if needed — never as body headings.

## Reading level (LOCKED — Ivan)
Write every Mansoor script at a **5th-grade reading level**:
- Plain words a middle-schooler gets on first hear
- Short sentences; easy to say out loud on camera
- No jargon, no fancy synonyms, no dense clauses
- If a word needs explaining, cut it or swap for a simpler one
This is a hard quality gate with voice/ICP rules — fail closed and rewrite if the draft reads above that level.
