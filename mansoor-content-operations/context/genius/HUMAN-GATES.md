# Human gates

## Gate A — candidate approval

The agent submits a batch-ranked ledger. Each candidate must include source timestamps, verbatim hook, promised value, delivery, context dependency, estimated engineered duration, risk, and score. Human response must name approved IDs. Only approved IDs enter message engineering.

## Gate B — headline approval

For each engineered candidate, the agent submits at least ten headline options with promise, evidence basis, character/line estimate, and score. The original suggestion may win. Human response must name one approved option or supply a replacement. No review render before this gate unless the job brief explicitly waives it.

## Gate C — exception approval

Required for any deliberate deviation from source-supported claims, style spec, duration/platform constraints, safe zones, or export spec. Log exception, reason, scope, approver, and date.

## Batch behavior

Gates should be batched to reduce interruption. Approval applies only to the listed candidate and version. A new cut or materially altered headline returns to the relevant gate.

