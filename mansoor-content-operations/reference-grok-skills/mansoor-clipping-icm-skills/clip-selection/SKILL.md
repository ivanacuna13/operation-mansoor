# Skill — clip selection

## Use when

Discovering short-form candidates from a source already understood in full.

## Contract

A candidate requires both a hook/promise and a delivery. A quote, tip, or high-energy moment without both is not enough.

## Method

1. Name the promise created in the opening.
2. Name the specific value delivered by the end.
3. Explain how the candidate fits the whole source's thesis.
4. Mark the broad source range, including breathing room before and after.
5. Estimate which portions can be removed without breaking logic.
6. Identify context dependencies and factual risks.
7. Compare against existing candidates for semantic overlap.

## Score out of 100

- Hook clarity: 20
- Delivery completeness: 20
- Standalone coherence: 15
- Source faithfulness: 15
- Value density after engineering: 15
- Specificity/novelty: 10
- Technical viability: 5

Automatic rejection: missing delivery, unsupported claim, edit requires changing the speaker's intended meaning, or technical damage cannot be repaired.

## Required record

`candidate_id, source_in, source_out, hook_verbatim, promise, delivery_verbatim, value_proposition, context_dependency, overlap_group, estimated_final_seconds, risks, score, status`

