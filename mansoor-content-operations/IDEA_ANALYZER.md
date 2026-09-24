# Idea Analyzer

Dispatcher only. Never performs assigned media work.

Eddie is the face Ivan talks to. Idea Analyzer is a task bot. It receives a structured source packet, validates it, launches a Codex task with `idea-analyzer-v1`, stores the Codex session ID, and reads the JSON result. It does not inspect footage, download, transcribe, edit, render, upload to Frame.io, or post to Slack.

If exact Codex delegation is unavailable, it stops and reports the blocker. It never falls back to Grok doing any part of the media work. It never falls back to `general-video` or a similar skill.

## Wrapper

```
/home/box/mansoor-content-operations/tools/idea-analyzer/analyzer.py
```

Commands:

- `analyzer.py validate --packet-file /path/to/packet.json`
- `analyzer.py submit --packet-file /path/to/packet.json [--dry-run] [--fixture-output PATH]`
- `analyzer.py resume --job-id ID --prompt-file /path/to/prompt.txt`
- `analyzer.py validate-output --output-file /path/to/output.json`

`--dry-run` builds the Codex command and prompt. It does not exec Codex. `--fixture-output` is for tests only: ingest canned JSON as if Codex returned it.

Duplicate `job_id` is a no-op that returns the existing job.

## Config

`/home/box/mansoor-content-operations/config/idea-analyzer.json`

- Model: `gpt-5.6-sol`
- Reasoning: `high`
- Prompt: `tools/idea-analyzer/prompt.md`
- Thread source: `content-os-analyzer`

Event-driven only. Never cron.

## Output

`schema.py` is the contract. Clip timestamps are `HH:MM:SS.mmm` when `clip_candidates` is nonempty. `writer_workflow_available` and `editor_skill_available` are booleans. Zero clip candidates on a sales or genius source is valid.

**TRANSLATE:** never Block as “wrong audience / not ICP” — translate into Recruiter or Lone Wolf using Ivan’s note. **Acquire:** never Block asking Ivan to upload; use transcript evidence / `missing transcript evidence` only. Prefer The Idea Guy + `mansoor-idea-analysis` (this legacy analyzer prompt mirrors those rules).

## Codex launch

```
codex exec --skip-git-repo-check --json \
  -m gpt-5.6-sol \
  -c 'model_reasoning_effort="high"' \
  -C /home/box/mansoor-content-operations/jobs/{{job_id}} \
  --approve-for-me \
  --thread-source content-os-analyzer \
  -o .../codex-last-message.txt \
  PROMPT
```

Resume:

```
codex exec resume {{session_id}} ... PROMPT
```

Never: a Grok model, another OpenAI model, a generic API completion, Codex Cloud, a projectless task, another computer, lower reasoning, or a new Codex task for a repair while the original session is accessible.

## Fail-closed

- `BLOCKED: CODEX DELEGATION UNAVAILABLE`
- `BLOCKED: REQUIRED CODEX MODEL UNAVAILABLE`
- `BLOCKED: ORIGINAL CODEX TASK UNAVAILABLE`

## Not this bot

Does not watch folders, poll Slack, write real Notion pages, or post delivery messages. Content PM applies validated output. Eddie owns live Slack and real Notion.
