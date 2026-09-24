# Pilot status — 2026-09-08

## Done (infrastructure + dry pilot)
- Inventory, 4-type docs align, Slack reaction allowlist
- Numbered layout helper + revision_identity live write path
- success_layers delivery-gate (worker cannot set approved)
- Self-attest QC quarantine; Frame stack-head helper; skill pointers
- Batch ownership stub; model/effort logging; Grok fallback fail-closed
- **Synthetic identity pilot PASS** (artifact: `pilot-synthetic/`):
  - gate rejects worker `approved=true` → `BLOCKED: WORKER_SET_APPROVED`
  - record gated revision → record delivered revision → human ✅ sets `current_approved_revision`
  - numbered tree created without moving media

## Not done (intentional / blocked)
1. **Live Codex + Frame media pilot** on a real new scripted batch / multi-clip sales call — would launch editors and may upload; waiting for a **new** assigned job (will not rewrite approved edits or publish unsolicited replacements).
2. **Premiere/AME on Mini** — paused (no Screen Recording / CC install path this run).
3. Workers on **live** jobs must emit `success_layers` + evidence (prompted; unproven in production until next real revise).
4. Analysis-cache reuse in real intake (stub only).
5. Lifestyle stays Eddie-owned.

## How to run next live pilot
Assign a fresh MVE packet (not an approved stack rewrite). After Codex returns, confirm:
- `jobs/<id>/00_admin/pointers.json` updated
- `mve.py identity-status --job-id <id>`
- delivery-gate refuses collapsed `qc_passed` without success_layers
- Frame `resolve_stack_head` called before comments/upload
