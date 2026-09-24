# MVE resume status (2026-09-08)

## 1. Implemented and tested
- Inventory, 4-type registry docs, reaction allowlist (sf-video + historical content-team + legacy ai-content-team; lifestyle ignored)
- Numbered layout helper, revision_identity live write path, synthetic identity pilot
- success_layers gate; self-attest quarantine; Frame stack-head helper; skill pointers to AGENTS_PROJECT_RULES
- Mini Adobe **installed** (Premiere/AME 26.3.2, Photoshop 27.10.0) — SSH + GUI session verified
- Config/dispatcher require `gpt-6-astra` / `medium`; fail string `BLOCKED: GPT-6-ASTRA MEDIUM UNAVAILABLE`
- **Astra dry worker PROVEN**: session `01a08116-388c-7a23-bf72-27a881fb0a28` rollout shows model=`gpt-6-astra`, effort=`medium` (see `astra-dry-proof.json`)


## Stage 1 (proven)
- Evidence: `adobe_bridge_evidence/stage1_mini_inventory.json`, `stage1_echo_result.json`
- Premiere 26.3.2, AME 26.3.2, Photoshop 27.10.0; GUI ivanclawd; ~57.6 GiB free
- Harmless echo submit/result via `/Users/ivanclawd/mve-adobe/queue` → `results`
- Automation probe: osascript yes; CEP/UXP system paths exist; **ffmpeg missing on Mini**
- AME process was already running at probe time

## 2. Implemented but not yet proven
- Operational Adobe bridge (building)
- Proxy-first behavior
- Real batch queue beyond advisory lock

## 3. Blocked (with evidence)
- (none external yet — Premiere is installed; prior “installing” status was stale and corrected)

## 4. Remaining work
- Prove Astra dry worker
- Stages 1–5 Adobe bridge smokes
- Stage 6 only with assigned production job
- Scheduler suite 6/14 investigation
