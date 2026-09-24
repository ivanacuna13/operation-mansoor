# Codex Skill Hardening Task

Grok coordinates only. You (Codex) perform skill hardening. Do not invent Frame credentials.
Do not post to Slack. Fail closed when a mandatory check fails.

## Packet
```json
{
  "revision_event_id": "rev_ver_9",
  "skill_name": "mansoor-first-draft-writer",
  "defect_category": "CTA formatting",
  "classification": "format_rule",
  "root_cause": "Writer skill lacked CTA capitalization automated check.",
  "measurable_rule": "CTA must use required capitalization.",
  "proposed_automated_check": "assert_cta_capitalization_format",
  "ivan_notes": "fix CTA capitalization — apply going forward",
  "promote": true
}
```

## Required steps (all 15)
1. Read the full revision chain (original output, Ivan notes, Frame.io timestamps if any, revised output, approval).
2. Determine root cause — why the process allowed the failure (not merely append Ivan's sentence).
3. Write a measurable permanent rule (objective pass/fail criteria).
4. Design an automated check that fails closed when the mandatory condition fails.
5. Create a regression fixture that recreates the failure and expects a block before delivery.
6. Update the exact target skill (Mansoor / format / system) — never general-video.
7. Bump skill version and update changelog in the skill folder.
8. Run the skill's tests / regression fixture; fail closed on failure.
9. Install updated skill on Linux Codex skills root.
10. Install / sync updated skill on Mac (or record mac_hash_status=pending with reason).
11. Compute and compare Linux hash vs Mac hash placeholders in skill-versions.json.
12. Update config/skill-versions.json (skill name, version, canonical location, hashes, last updated, revision event id, test result, installed status).
13. Write accepted rule file under learning/accepted-rules/.
14. Append or update the human Rules Learned From Revisions entry (plain English only).
15. Return packet with promotion result; do not claim Mac sync if pending.

## Constraints
- Root cause must explain why process allowed failure — do not merely append Ivan's sentence.
- Never auto-universalize a one-video creative preference.
- Never fall back to general-video.
- Update skill-versions.json hashes; Mac may remain pending.
- Write accepted rule under learning/accepted-rules/.
