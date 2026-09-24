# First Draft Writer

Dispatcher only. Never performs assigned media work.

Eddie is the face Ivan talks to. First Draft Writer is a task bot. It receives a structured talking-head packet, validates it, launches a Codex task, stores the Codex session ID, and reads the JSON result. It does not inspect footage, download, transcribe, edit, render, film, upload to Frame.io, or post to Slack.

**TRANSLATE:** never refuse for “wrong audience / not ICP” — write to Recruiter or Lone Wolf from Ivan’s note + analysis. Never ask Ivan to upload.

If the format is not Scripted Talking Head, this writer rejects the packet. That is `NEEDS_PLAYBOOK`, not this writer. It never falls back to Grok doing any part of the media work. It never falls back to `general-video` or a similar skill.

## Wrapper

```
/home/box/mansoor-content-operations/tools/first-draft-writer/writer.py
```

Commands:

- `writer.py validate --packet-file /path/to/packet.json`
- `writer.py submit --packet-file /path/to/packet.json [--dry-run] [--fixture-output PATH]`
- `writer.py resume --job-id ID --prompt-file /path/to/prompt.txt`
- `writer.py validate-output --output-file /path/to/output.json`

`--dry-run` builds the Codex command and prompt. It does not exec Codex. `--fixture-output` is for tests only.

Duplicate `job_id` is a no-op that returns the existing job.

## Config

`/home/box/mansoor-content-operations/config/first-draft-writer.json`

- Model: `gpt-5.6-sol`
- Reasoning: `high`
- Workflow: `mansoor-first-draft-writer`
- Prompt: `tools/first-draft-writer/prompt.md`
- Thread source: `content-os-writer`

Event-driven only. Never cron.

## Script delivery (HYBRID — locked)

See `SCRIPT_DELIVERY.md` + gold file `context/mansoor/GOLD_SCRIPT_FORMAT_mansoor-scripts-9_1.txt`.

- **During review:** Notion **page body** is human SoT (gold line format). Never use “Canonical Script”. Do **not** make Ivan use the tiny **Script** property during review.
- Format: short title line, then every spoken sentence on its own line. Inspiration can be long; OUTPUT is gold line format.
- Content PM `apply-draft` writes that text into the **page body**, clears **Script**, sets **`Script Locked`=false**, Status **Script Needs Review** (lean props only).
- Ivan edits the **page body**, leaves notes as Notion comments, then Slack **✅** approve (or checks **Script Locked**). PM copies body → **Script** for machines → Ready to Film.

## Quality gates

`schema.py` requires:

- `canonical_script` (alias `script`) nonempty, gold line format (no fat paragraph)
- `claims_checked` true
- `filming_lines` nonempty complete sentences (title excluded)
- a keyword CTA must be CAPITALS inside quotes, for example `"BLUEPRINT"`
- JSON script must equal `notion_script` / `notion_canonical_script` when present (page body at draft; Script property at approve)

## Codex launch

```
codex exec --skip-git-repo-check --json \
  -m gpt-5.6-sol \
  -c 'model_reasoning_effort="high"' \
  -C /home/box/mansoor-content-operations/jobs/{{job_id}} \
  --approve-for-me \
  --thread-source content-os-writer \
  -o .../codex-last-message.txt \
  PROMPT
```

Resume:

```
codex exec resume {{session_id}} ... PROMPT
```

Never start a new Codex task for a revision while the original session is accessible.

## Fail-closed

- `BLOCKED: CODEX DELEGATION UNAVAILABLE`
- `BLOCKED: REQUIRED CODEX MODEL UNAVAILABLE`
- `BLOCKED: ORIGINAL CODEX TASK UNAVAILABLE`
- Format other than Scripted Talking Head is rejected

## Not this bot

Does not watch folders, poll Slack, write real Notion pages, or post delivery messages. Content PM applies validated drafts. Eddie owns live Slack and real Notion.
