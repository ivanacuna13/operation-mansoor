# Review-Learning Compiler — design proposal

Status: approved in principle and revised for the Shared Content Intelligence Core; not an implemented skill, not an activated rule system, and not an authorization to modify permanent instructions.

Updated: 2026-09-09

> Controlling contract: [`../UNIFIED_CONTENT_INTELLIGENCE_CORE_DESIGN.md`](../UNIFIED_CONTENT_INTELLIGENCE_CORE_DESIGN.md) defines final shared-table ownership, IDs and the cross-module event contract. This compiler remains a bounded module in that one PostgreSQL database.

## Purpose and non-negotiable invariant

The compiler turns review history into evidence-backed institutional memory while preserving this chain:

`raw feedback -> source/context -> interpretation -> revision -> approval/rejection -> published result -> performance validation -> resulting lesson`

Raw feedback is immutable. A later correction, interpretation, dispute, or deletion creates another event; it never overwrites the capture. Unknown information remains `unknown` with a reason. Inference is stored separately from observation.

The compiler may extract, link, cluster, score, and propose. It may not silently rewrite permanent instructions, infer approval from ordinary conversation, or universalize a strongly worded isolated opinion.

## 1. System architecture

```text
Slack / Codex / Asana / Markdown / review tools / manual notes / performance
                                |
                         source adapters
                                |
               immutable raw evidence store (content + hash)
                                |
               normalization and identity-resolution queue
                                |
                  feedback-event / revision lineage graph
                                |
           interpretation + taxonomy + contradiction detection
                                |
                      lesson-candidate registry
                                |
        evidence aggregation + confidence + promotion state machine
                                |
       output projections / proposals / preflight rule candidates
                                |
                 human approval and documentation PR trail
```

### Architectural components

1. **Source adapters** acquire source-native IDs, URLs, timestamps, authors, message text, attachments, reactions, comment timecodes, task IDs, and deletion/edit metadata.
2. **Raw evidence store** keeps the exact acquired payload and, where allowed, a rendered text snapshot. Each capture receives a SHA-256 hash. Source edits create new capture revisions.
3. **Normalizer** maps platform-specific material into feedback events without replacing the raw payload.
4. **Identity and lineage resolver** links task, project, concept, reel, source asset, render, review version, publication, and performance snapshots. Ambiguous matches enter a queue.
5. **Interpreter** creates one or more explicitly inferred claims from a feedback event. Interpretations are versioned and attributable to a model or human.
6. **Evidence graph** connects feedback to revisions, decisions, publications, outcomes, supporting events, contradicting events, and documents.
7. **Lesson engine** clusters related interpretations, applies scope and promotion gates, and produces candidates—not direct doctrine edits.
8. **Output projectors** build the ten requested operational views from the same canonical evidence.
9. **Approval service** records proposed change, approver, decision, rationale, exact diff, effective date, and rollback/supersession link.

### Source-of-truth boundary

- The Trial Reel Laboratory's canonical PostgreSQL database is the only structured system of record. The compiler is a bounded PostgreSQL schema inside that database, not a second database.
- The raw evidence object is the source-of-record for what was actually said or observed.
- The Shared Content Intelligence Core owns creative families, versions, renders, publications, performance snapshots, human reviews, source assets/segments, and audio/copy/B-roll manifests. The compiler references those rows through real foreign keys and never creates local copies.
- Operational Markdown/skills are approved projections, not the evidence store.
- Performance never retroactively changes the raw feedback or approval event. It adds validation or contradiction evidence.

## 2. Database schemas

Use the same canonical PostgreSQL cluster, backup/restore policy, immutable object store, restricted roles, and hash-chained audit ledger specified by [the Trial Reel Laboratory design](../reports/MANSOOR_TRIAL_REEL_LABORATORY_DESIGN.md). The compiler owns the `review_learning` schema. Shared objects live in `content_core` (the final schema name may differ, but ownership may not). Store large raw payloads and screenshots in the shared content-addressed object store and retain their hashes in PostgreSQL. All decisions and state changes append events; current-state views are rebuildable projections. There is one shared typed-ID service/registry, not a compiler-specific allocator.

### 2.1 Ownership boundary

| Shared Content Intelligence Core owns | Review-Learning Compiler owns |
| --- | --- |
| Ideas and creative families (`IDE_`, `FAM_`) | Source captures (`CAP_`) |
| Hypotheses/experiments when formally registered (`HYP_`, `EXP_`) | Raw feedback events (`FBK_`) |
| Immutable versions/change sets (`VER_`, `CHG_`) | Interpretations (`INT_`) |
| Renders and QC (`RND_`) | Evidence-origin groups (`ORG_`) |
| Publications (`PUB_`) | Contradiction clusters (`CFL_`) |
| Performance snapshots (`SNP_`) | Lesson candidates (`LSN_`) |
| Human reviews (`REV_`) | Confidence/evidence-state events (`EST_`) |
| Source assets/segments (`MED_`, `SEG_`) | Promotion decisions (`PMD_`) |
| Audio and copy/B-roll manifests (`AUD_` and the Core's canonical manifest IDs) | Approved rules (`RUL_`) |
| People/accounts/workflow/ICP registries and operational incidents | Documentation-change proposals (`DCP_`) |

The compiler must not make a “local family,” “feedback version,” “review render,” “published outcome,” asset row, or copied audio manifest. If a referenced shared object is missing, the compiler stores the external alias in the capture and creates an ambiguity/linkage item. It does not allocate a substitute Core ID.

Cross-schema foreign keys are mandatory wherever the shared object exists. A text field that merely looks like `VER_...` is not sufficient.

### 2.2 Permanent ID contract

Use the Trial Reel Laboratory contract: an uppercase type prefix, underscore, and a 26-character Crockford Base32 ULID. `created_at` remains authoritative; the sortable timestamp inside the ULID is not business time.

Compiler prefixes:

- `CAP_<26-char-ulid>` — source capture
- `FBK_<26-char-ulid>` — atomic raw feedback event
- `INT_<26-char-ulid>` — interpretation revision
- `ORG_<26-char-ulid>` — independent evidence-origin group
- `CFL_<26-char-ulid>` — contradiction/conflict cluster
- `LSN_<26-char-ulid>` — lesson candidate
- `EST_<26-char-ulid>` — evidence/confidence state event
- `PMD_<26-char-ulid>` — promotion decision
- `RUL_<26-char-ulid>` — approved rule
- `DCP_<26-char-ulid>` — documentation-change proposal

Shared references retain their existing Core IDs, including `FAM_`, `VER_`, `RND_`, `PUB_`, `SNP_`, `REV_`, `MED_`, `SEG_`, and `AUD_`. External IDs—Slack timestamps, Drive IDs, Frame comment IDs, filenames, Notion IDs, Asana GIDs, Codex task IDs, Instagram shortcodes—remain aliases and never become primary keys.

Required database checks:

- prefix and Crockford alphabet/length check for each owned ID;
- no ID reuse after rejection, supersession, or source deletion;
- immutable creation row plus superseding event instead of semantic mutation;
- idempotency key unique by adapter and source event;
- Core FK constraints are `RESTRICT`, not silent cascade deletion;
- compiler roles have `SELECT` on required Core tables and no permission to allocate or mutate Core creative/media identities.

### 2.3 Compiler-owned evidence schema

#### `source_captures`

| Field | Type | Meaning |
| --- | --- | --- |
| `capture_id` | text PK | Permanent `CAP_` ID under the shared ULID contract. |
| `platform` | enum | `slack`, `codex`, `asana`, `markdown`, `frameio`, `review_tool`, `manual`, `instagram`, other. |
| `source_native_id` | text | Slack `channel:ts`, Codex task/turn ID, Asana story/task ID, file+line anchor, Frame comment ID, etc. |
| `canonical_url` | text nullable | Native deep link when available. |
| `captured_at` | timestamp | Compiler acquisition time. |
| `source_created_at` | timestamp nullable | Native event time. |
| `source_edited_at` | timestamp nullable | Native edit time. |
| `author_native_id` / `author_display` | text | Preserve both stable identity and displayed name. |
| `core_actor_id` | nullable FK -> Core people/actors | Canonical identity when resolved; native author fields remain part of raw provenance. |
| `raw_mime_type` | text | JSON, Markdown, text, image, etc. |
| `raw_blob_uri` | text | Content-addressed immutable payload. |
| `raw_sha256` | text | Tamper/dedupe check. |
| `capture_revision` | integer | Monotonic revision for edited source material. |
| `deleted_at_source` | boolean | Tombstone only; raw capture remains. |
| `access_scope` | text | Workspace/channel/project and privacy boundary. |
| `ingestion_method` | text | Connector, webhook, poll, filesystem watcher, manual form, import. |
| `parser_version` | text | Reproducibility. |
| `source_context` | JSON | Native task/project/channel/file aliases exactly as observed; resolved canonical relationships live in Core FKs/views. |

Unique key: `(platform, source_native_id, capture_revision)`. Identical hashes dedupe storage, not logical events.

#### `raw_feedback_events`

This is the atomic observation requested for every feedback item. One source message can yield multiple events when it contains independent comments; each retains the same raw capture and a verbatim span. It does not own approval, revision, render, publication, performance, asset, or audio state.

| Field | Type | Meaning |
| --- | --- | --- |
| `feedback_id` | text PK | Permanent `FBK_` ID. Never recycled. |
| `capture_id` | FK -> `review_learning.source_captures` | Immutable source capture. |
| `origin_group_id` | FK -> `review_learning.evidence_origin_groups` | Independent-origin accounting. |
| `shared_review_id` | nullable FK -> `content_core.human_reviews.review_id` | Canonical `REV_` event when the Core has typed the human review. The compiler never duplicates its decision. |
| `family_id` | nullable FK -> Core `creative_families` | Canonical creative family, never a local family. |
| `version_id` | nullable FK -> Core `versions` | Exact reviewed creative spec when known. |
| `render_id` | nullable FK -> Core `renders` | Exact reviewed artifact when known. |
| `publication_id` | nullable FK -> Core publications | Only when feedback targets an actual deployment. |
| `source_platform` | generated/view | Read from capture, not independently mutable. |
| `source_message_url_or_identifier` | generated/view | Read from capture. |
| `feedback_timestamp` | timestamp nullable | Native timestamp, not ingestion time. |
| `raw_feedback` | text | Verbatim span; immutable. |
| `raw_span` | JSON | Character/line bounds inside capture. |
| `referenced_timestamp_or_visual` | JSON nullable | Timecode/range, frame, screenshot, or asset reference. |
| `event_kind` | enum | revision request, approval reason, rejection reason, observation, question, availability report, technical finding. |
| `link_status` | enum | `unlinked`, `candidate`, `linked`, `ambiguous`, `conflicted`. |
| `parser_version` | text | Extraction reproducibility. |

The full user-facing feedback record is a view joining this row to `source_captures`, the latest `feedback_interpretation`, Core `REV_`/`VER_`/`RND_`/`PUB_`/`SNP_` records, lesson evidence, workflow/ICP registries, and conflict edges. Requested revision, inferred reason, action taken, before/after versions, approval status, publication status, performance outcome, confidence, and applicability are therefore visible without duplicating their canonical owners.

#### `feedback_interpretations`

- `interpretation_id` PK (`INT_`), `feedback_id` FK, `supersedes_interpretation_id` nullable FK;
- `requested_revision`, `inferred_reason`, `normalized_claim`, `target_taxonomy`, `failure_mode`;
- `applicable_workflow_ids`, `applicable_icp_ids`, and conditional scope through join tables;
- `interpreter_type`, `interpreter_id_or_model`, `interpreter_version`, `created_at`;
- `status` (`machine_draft`, `human_validated`, `disputed`, `superseded`).

Interpretations never update raw feedback.

#### `evidence_origin_groups` and `evidence_origin_members`

- Group ID `ORG_`, canonical first capture/event, grouping basis, confidence, status, human validation.
- Member points to `CAP_` and optionally `FBK_`, with relationship `original`, `mirror`, `quote`, `summary`, `derived_documentation`, or `unknown`.
- Only one independent-origin unit per group may count toward repetition thresholds.
- Same hash is strong duplicate evidence but not required; a paraphrase in `MISTAKES.md` may still derive from one Slack comment.

#### `contradiction_clusters` and `contradiction_members`

- Cluster ID `CFL_`, normalized issue axis, current status, scope matrix, owner, review trigger, resolution type.
- Members link `INT_`/`LSN_` with stance, context, Core version/render/review/publication/snapshot references, and whether the conflict is truly opposing or merely differently scoped.

### 2.4 Lesson, evidence, decision, and rule schema

#### `lesson_candidates`

| Field | Type | Meaning |
| --- | --- | --- |
| `lesson_id` | text PK | Permanent `LSN_` ID under the shared contract. |
| `canonical_claim` | text | Testable, scoped statement—not copied rhetoric. |
| `lesson_class` | enum | The required five-class model below. |
| `rule_domain` | enum | privacy, legal, religious, technical, headline, edit, audio, B-roll, workflow, delivery, performance, other. |
| `polarity` | enum | require, prefer, avoid, prohibit, investigate. |
| `scope_workflows`, `scope_icps` | join tables | Explicit applicability. |
| `scope_conditions` | JSON | Content type, emotional beat, duration, platform, reviewer, era, etc. |
| `status` | enum | `candidate`, `emerging`, `proposed`, `approved`, `rejected`, `experimenting`, `deprecated`, `superseded`. |
| `evidence_summary` | text | Human-readable synthesis. |
| `confidence_vector` | JSON | Fidelity, causal linkage, replication, approval, performance, recency, contradiction. |
| `confidence_score` / `band` | number/enum | Convenience only; never the sole promotion gate. |
| `first_seen_at`, `last_seen_at` | timestamp | Recency/outdated-rule checks. |
| `owner` | text | Accountable human. |
| `review_due_at` | timestamp | Sunset/revalidation date. |
| `supersedes_lesson_id` | FK nullable | History remains navigable. |

#### `lesson_evidence`

Many-to-many link from a lesson to feedback, decisions, revision actions, technical findings, publications, and performance snapshots. Each edge records:

- `stance`: support / contradict / context-only;
- `origin_group_id` FK: prevents three copies of one Slack message from counting as three observations;
- `causal_strength`: unlinked / correlated / before-after / controlled comparison;
- `weight_reason`: transparent explanation, not just a number;
- nullable Core FKs: `REV_`, `VER_`, `CHG_`, `RND_`, QC/incident IDs, `PUB_`, `SNP_`, `MED_`, `SEG_`, `AUD_`, plus experiment/conclusion and manifest IDs where present;
- `added_by` and `added_at`.

#### `evidence_state_events`

`EST_` rows append the confidence vector, evidence-stage result, threshold evaluation, missing evidence, contradiction penalty, stale-rule signals, evaluator/version, and timestamp. The current confidence is a view over the newest accepted `EST_`; prior scores remain visible.

#### `promotion_decisions`

`PMD_` rows record candidate, requested transition, outcome (`defer`, `promote`, `reject`, `narrow`, `demote`, `supersede`), deciding human/service, authority basis, evidence-state ID, rationale, timestamp, and superseded decision. A classifier recommendation is not a promotion decision.

#### `approved_rules`

`RUL_` rows exist only after an authorized promotion decision. They store lesson ID, exact scoped rule, class, severity (`inform`, `warn`, `block`), workflow/ICP/condition scope, exceptions, effective/review dates, approver, and lifecycle state. Machine-readable preflight JSON is compiled from this table; the compiler does not treat a candidate file as an active rule.

#### `documentation_change_proposals`

| Field | Type | Meaning |
| --- | --- | --- |
| `proposal_id` | text PK | Permanent `DCP_` change request. |
| `lesson_id` | FK | Evidence-backed lesson. |
| `approved_rule_id` | nullable FK | Required when proposing to encode an already approved rule. |
| `target_document` | text | Exact path/skill/config. |
| `target_section` | text | Stable section ID or heading. |
| `base_hash` | text | Prevent stale overwrite. |
| `proposed_diff` | text | Reviewable patch. |
| `impact` | enum | advisory, workflow, preflight-blocking, privacy/legal. |
| `requested_by`, `requested_at` | text/time | Audit trail. |
| `approval_status` | enum | `draft_shadow`, `draft`, `pending`, `approved`, `rejected`, `superseded`, `implemented`, `rolled_back`. |
| `approver`, `decision_at`, `decision_reason` | nullable | Required for material changes. |
| `implementation_hash` | text nullable | Exact installed result. |

The shadow pilot may populate proposals only with `approval_status=draft_shadow`. It must not create `implemented` events, update target files, write accepted-rule projections, or compile active preflight rules.

## 3. Classification model

Classification occurs on the lesson, not directly on the emotional wording of the source comment.

1. **Hard constraint** — non-negotiable restriction grounded in explicit authorized privacy, religious, legal, safety, identity, security, or publication instruction. Example: wife face must not be exposed. It is immediately active in the appropriate scope, but still requires source citation and an approval trail when encoded into permanent documents.
2. **Proven production rule** — a reusable causal or quality rule supported by independent revision chains, approval outcomes, and where relevant performance or deterministic QC. Example: frozen-frame padding is a delivery-blocking defect.
3. **Workflow-specific preference** — stable preference that is valid only for named formats, content families, reviewers, or ICPs. Example: an origin-to-lifestyle copycat opens on hardship evidence and ends on payoff imagery.
4. **Experiment hypothesis** — plausible creative claim that needs controlled or repeated evidence. Example: a shorter opener may improve retention on 6–15 second TOF edits.
5. **One-off creative direction** — instruction for one asset/version or a deliberately unique treatment. It remains searchable but does not enter preflight rules.

### Orthogonal tags

Each record also gets tags independent of lesson class:

- feedback intent: approval, rejection, revision, question, observation, technical finding, availability issue;
- target: hook/headline, first frame, pacing, B-roll, story, crop, captions, audio, color, privacy, identity, publication, delivery;
- failure mode: repeated shot, unavailable footage, unsafe identity exposure, freeze/flash, thin audio, dirty lyric, wrong person, weak picture-text match, incomplete payoff, unreadable text;
- evidence type: direct quote, reaction, artifact diff, machine measurement, approval decision, publication, performance;
- scope: workflow, template family, ICP, platform, duration band, emotional beat;
- observability: objective/measurable, subjective, mixed;
- causal status: requested only, implemented, approved after implementation, published, performance-tested.

Strong wording only increases `instruction_explicitness`; it does not increase replication, causal linkage, or generality.

## 4. Confidence and promotion rules

### Confidence vector

Keep the components visible:

- source fidelity: 0–20;
- exact version/context linkage: 0–15;
- revision-to-decision linkage: 0–20;
- independent replication: 0–20;
- publication/performance validation: 0–15;
- recency/relevance: 0–10;
- unresolved contradiction penalty: 0 to -25.

Bands: 0–24 very low, 25–44 low, 45–64 medium, 65–84 high, 85–100 very high. A score never bypasses class-specific gates.

### Evidence stages

| Stage | Minimum evidence | Allowed output |
| --- | --- | --- |
| Candidate | One authentic comment/finding linked to context. | Searchable candidate or one-off instruction. |
| Emerging | At least two independent review chains across at least two edits/content objects, or an explicit forward-looking preference plus one approved implementation. | Workflow warning; proposed experiment; never global blocking rule. |
| Proposed rule | At least three independent chains, two approved implementations, defined scope, no unresolved material contradiction. | Human-reviewable documentation/preflight proposal. |
| Proven rule | Proposed-rule evidence plus either two published outcomes supporting the mechanism, a controlled comparison, or deterministic repeated QC evidence where performance is irrelevant; named owner approves. | Approved playbook/preflight projection in its precise scope. |
| Deprecated/superseded | New contradictory evidence, changed platform/ICP/workflow, repeated failures, or owner decision. | Warning and migration proposal; history retained. |

### Special gates

- **Hard constraints:** one explicit instruction from an authorized owner concerning privacy/religion/legal/safety/security may activate immediately. Ambiguous remarks do not. Encode the source, authority, scope, and review date.
- **Technical blocking rules:** a reproducible defect can become a temporary fail-closed QC gate after one severe incident, but “proven production rule” status still requires verification that the test detects the actual failure without unacceptable false positives.
- **Creative preferences:** require replication. Approval alone shows acceptability, not causality. Performance alone shows correlation, not why a post won.
- **Performance claims:** compare against the account’s rolling baseline and the same workflow/ICP when possible. Do not treat source-post virality as validation of a Mansoor remake.
- **Negative evidence:** rejection without a linked version and reason is weak. A killed version with exact reasons is strong rejection evidence but still may contain several confounded changes.
- **Independence:** a Slack quote copied into `REVIEW_LOG.md`, `MISTAKES.md`, and a Codex task counts as one evidence origin, not three.

### Existing subsystem migration warning

The current `tools/learning` prototype should not be the final authority because it:

- marks broad “objective” categories for immediate promotion;
- can promote on wording such as “always” without enough context;
- stores raw notes and inferred permanent rules in one record;
- counts approved events by category/skill without strong independence or content lineage;
- rewrites `revision-events.jsonl` to mark items handled despite calling it append-only;
- writes accepted-rule files before a material human documentation approval trail is represented.

Its useful parts—event IDs, candidates, regression fixtures, and hardening packets—can be migrated behind the new evidence and approval model.

## 5. Conflict-resolution process

1. **Preserve both statements** and their raw captures.
2. **Normalize the claims** into comparable predicates, e.g. `increase_cut_rate` versus `preserve_pause_at_emotional_peak`.
3. **Build a context matrix:** workflow, ICP, duration, narrative beat, speaker emotion, reviewer role, version, exact time range, and intended outcome.
4. **Check lineage:** which instruction was implemented, partially implemented, declined, or made impossible by missing footage?
5. **Check the explicit decision:** which exact version was approved/rejected and by whom? Silence is not approval.
6. **Check publication and performance:** link the approved render to its actual post and normalized outcome. Avoid causal claims when multiple variables changed.
7. **Resolve by narrowing before choosing:** both rules may be valid in different contexts. “Fast baseline pacing; allow longer holds only on labeled emotional peaks” is a scoped synthesis, not a deletion of either comment.
8. **If unresolved, queue an experiment:** specify variants, held-constant elements, success metric, sample size/horizon, and stopping rule.
9. **If authority conflicts:** preserve all evidence, but route the operational decision to the named content owner. Reviewer hierarchy determines who decides, not whose evidence disappears.
10. **Reopen automatically** when a new approval, rejection, performance snapshot, workflow change, or stale-date trigger arrives.

For “speed up the edit” versus “let the emotional moment breathe,” the compiler should initially create a conflict cluster, not a global pacing rule. It should inspect whether the comments targeted connective tissue or an emotional peak, which revision won approval, and how the published version performed. The likely result is a conditional hypothesis, not a winner-takes-all rule.

## 6. Sample extractions from `REVIEW_LOG.md`

These are illustrative records. IDs are examples and would be generated once during an actual import.

### Sample A — origin opening

**Original feedback:** “Make opening shot more of when he was homeless”

```yaml
feedback_id: "FBK_<allocated-at-import>"
source_platform: slack
source_message_url_or_identifier: "thread_ts:1786931750.182009"
task_project: "Lifestyle Copycat / POV: you stuck with it"
reel_version_render_id: "v1 / Drive 1Cbc2KCvvwBDy_FTsFX0Z3ySNUhswLLd9"
reviewer: Ivan
timestamp: "2026-08-16 (exact source time to be resolved from Slack)"
raw_feedback: "Make opening shot more of when he was homeless"
referenced_timestamp_or_visual: "opening shot; exact timecode unknown"
requested_revision: "Replace the current-life opening with a visibly humble/origin image."
inferred_reason: "The phrase 'you stuck with it' needs credible before-state evidence."
action_taken: "Opened v2 on IMG_5004.JPG: Mansoor, sleeping bag, chairs, grocery bag."
before_version: "Drive 1Cbc2KCvvwBDy_FTsFX0Z3ySNUhswLLd9"
after_version: "Drive 17KOKI_VURiyGBBRlGsmA6nEjZQhfUX2R"
approval_status: "revision delivered; final explicit approval not present in REVIEW_LOG"
publication_status: unknown
performance_outcome: unknown
lesson_candidate: "Origin-transformation edits should open on specific hardship evidence."
confidence: medium
applicable_workflow: ["TOFU Copycat", "origin transformation"]
applicable_ICP: ["18-28 US recruit path"]
contradictions_or_related_feedback: ["stellar face-first guidance", "family-payoff winner evidence"]
```

Classification: **workflow-specific preference**, currently **emerging**, not a universal rule. It is directly implemented, agrees with the 190K origin mechanism and B-roll audit, but the log does not show this exact v2’s explicit approval or published performance.

Strengthen with: explicit approval of the exact v2; repeated approvals on other origin edits; 3-second retention and completion/share performance versus current-life openers. Overturn/narrow with: approved origin edits that intentionally open on present-day payoff and outperform, or evidence that the hardship image confuses a different ICP. Future workflows: origin-story assembler, TOFU copycat, documentary transformation, B-roll gap detector.

### Sample B — work must be visible

**Original feedback:** “Change second shot doesn't show him working. Want him working”

```yaml
feedback_id: "FBK_<allocated-at-import>"
source_platform: slack
source_message_url_or_identifier: "thread_ts:1786928716.330549"
task_project: "Lifestyle Copycat / Dad safe-path -> crazy-dream"
reel_version_render_id: "Drive 170sq26G4Uao-kwSLuHZtvahyf1jVh7xU"
reviewer: Ivan
timestamp: "2026-08-16 (exact source time to be resolved)"
raw_feedback: "Change second shot doesn't show him working. Want him working"
referenced_timestamp_or_visual: "second shot; B&W hallway with other people"
requested_revision: "Use a shot in which Mansoor is visibly performing work."
inferred_reason: "Generic hallway footage does not prove the work chapter in the causal story."
action_taken: "Replaced hallway with face_cafe.MOV, Mansoor at a MacBook in B&W."
before_version: "Drive 170sq26G4Uao-kwSLuHZtvahyf1jVh7xU"
after_version: "Drive 136YCReJ185-xof28iH1ktzUJ-P6yt8dg (latest logged recut)"
approval_status: "v1 was stellar/approved; revised version delivered; revised approval unknown"
publication_status: unknown
performance_outcome: unknown
lesson_candidate: "When a narrative beat claims work, use literal Mansoor-specific work evidence."
confidence: medium
applicable_workflow: ["TOFU Copycat", "Genius B-roll", "origin-to-proof edits"]
applicable_ICP: ["TOF youth recruit", "Recruiter", "Lone Wolf when work proof is claimed"]
contradictions_or_related_feedback: ["pictures follow the line", "work-footage library shortage"]
```

Classification: **workflow-specific preference** with a broader **experiment hypothesis** about picture-text congruence. It should not yet become “always show Mansoor working in shot two.”

Strengthen with: approval of revised versions, repeated rejection of generic work proxies, performance/retention comparisons, or eye-tracking/comprehension evidence. Overturn/narrow with: approved metaphorical work visuals in audio-led edits or contexts where literal laptop footage reduces emotion. Future workflows: copycat editor, Genius B-roll, beat mapper, shoot list.

### Sample C — opening duration

**Original feedback:** “The first shot was held for too long”

```yaml
feedback_id: "FBK_<allocated-at-import>"
source_platform: slack
source_message_url_or_identifier: "thread_ts:1786933899.177169"
task_project: "Lifestyle Copycat / POV: how life starts to feel around good people"
reel_version_render_id: "Drive 1W7aFD0EYmyxj7EyDj-4ABdl1IThhRl1V"
reviewer: Ivan
timestamp: "2026-08-16 (exact source time to be resolved)"
raw_feedback: "The first shot was held for too long"
referenced_timestamp_or_visual: "first shot; exact duration not present in log"
requested_revision: "Shorten opening shot and cut to different footage sooner."
inferred_reason: "The hold felt slow or visually stale in this edit."
action_taken: unknown
before_version: "Drive 1W7aFD0EYmyxj7EyDj-4ABdl1IThhRl1V"
after_version: unknown
approval_status: revision_requested
publication_status: unknown
performance_outcome: unknown
lesson_candidate: "Test shorter first-shot holds for short lifestyle copycats."
confidence: low
applicable_workflow: ["Lifestyle Copycat"]
applicable_ICP: ["18-28 US recruit path"]
contradictions_or_related_feedback: ["emotional moments may require longer holds", "never repeat/loop shots"]
```

Classification: **experiment hypothesis**, not a rule. The source lacks the original duration, revision, approval, and performance.

Strengthen with: measured before/after hold lengths, exact approved v2, repeated comments across edits, and first-3-second retention. Overturn/narrow with: high-performing approved long holds when the image or emotion justifies them. Future workflows: Lifestyle Copycat first-frame/pacing preflight and trial-reel laboratory.

### Sample D — quality crash

**Original feedback:** “super shit audio, bad text hooks, frozen frames.”

This must be split into three feedback records sharing one capture because each has different verification and remedies.

- **Frozen frames:** technical finding plus explicit rejection. Classification: temporary hard QC gate immediately; candidate proven production rule after reproducing the detector on actual failures and checking false positives. Evidence is strengthened by machine-detected freezes across several renders and QC-passed recuts with none. Applicable to every motion-video workflow; photo still exceptions remain explicit.
- **Audio quality:** proven-production candidate scoped to delivery quality, not “all sub-80 kbps audio is always bad.” Human listen remains required because codec/bitrate is a proxy. Strengthened by four dirty-vocal swaps and successful clean replacements; overturned/narrowed by perceptually clean low-bitrate sources.
- **Bad text hooks:** experiment/workflow preference until the exact rejected hook characteristics are independently replicated. The killed reel changed audio, hook, and motion quality simultaneously, so performance or rejection cannot isolate headline causality.

The split prevents one forceful rejection from turning three confounded complaints into three universal doctrines.

## 7. Weekly learning digest template

```markdown
# Review-Learning Digest — YYYY-MM-DD to YYYY-MM-DD

## Decision summary
- New hard constraints awaiting/receiving owner confirmation:
- Proven-rule proposals ready for approval:
- Emerging workflow patterns:
- Experiments to run:
- Conflicts requiring a decision:

## Evidence health
- Sources scanned / captures added / parse failures:
- Feedback linked to exact render: __%
- Feedback with explicit decision: __%
- Published renders with performance snapshots: __%
- Unresolved identity/version links:

## Repeated rejection reasons
| Pattern | Independent chains | Workflows | Latest evidence | Proposed response |

## Repeated approval reasons
| Pattern | Independent chains | Workflows | Performance support | Proposed response |

## Performance validation
| Lesson/hypothesis | Published variants | Baseline | Result | Supports/contradicts/inconclusive |

## Conflicts and stale rules
| Conflict/rule | Contexts | Current evidence | Owner/question | Review due |

## B-roll intelligence
- Rating upgrades/downgrades proposed:
- Overused/fatigued assets:
- Privacy/identity failures:
- Requested but unavailable footage:
- Prioritized shoot list:

## Technical and delivery failures
| Failure | Count | Affected versions | Detector coverage | Action |

## Documentation proposals
| Proposal | Lesson | Target doc | Materiality | Approver | Status |

## Next-week experiments
| Hypothesis | Variants | Held constant | Metric/horizon | Stop rule | Owner |

## Appendix: source links
- Every item links to immutable feedback IDs and native sources.
```

## 8. Documentation-update workflow

1. Lesson reaches `proposed` through evidence gates or an authorized hard-constraint event.
2. Compiler identifies impacted documents and exact headings using a document registry.
3. It generates a patch against a recorded base hash, plus rationale, supporting and contradicting feedback IDs, scope, confidence, and regression/preflight implications.
4. Non-material wording/clarity changes may use a lightweight owner review. Material creative rules, new blocking checks, privacy/legal/religious instructions, workflow authority changes, and deletions require named owner approval.
5. Approval records the exact diff. Rejection records a reason and leaves the lesson/evidence intact.
6. An implementation worker applies only the approved patch, verifies the resulting hash, and runs relevant tests.
7. The registry records effective version/date and links the old rule. No history is erased.
8. If later contradicted, the compiler proposes deprecation, narrowing, or supersession; it never silently edits doctrine.

Suggested material approval chain:

`compiler proposal -> operations/editor review -> Ivan/content-owner approval -> implementation -> regression/preflight verification -> effective`

## 9. Output projections

1. **Hard-constraint registry:** active constraint, authority/source, exact scope, implementation coverage, exceptions, owner, review date.
2. **Proven creative playbook:** only approved proven production rules, with evidence and counterexamples.
3. **Workflow-specific guidance:** scoped preferences grouped by workflow/ICP/template family.
4. **Experiment backlog:** hypothesis, conflict, variants, metrics, horizon, priority, required footage, owner.
5. **B-roll rating updates:** asset/shot-level rating proposal, evidence IDs, privacy/identity flags, reuse/fatigue, approved status.
6. **Missing-footage/shoot list:** repeated requested story role, affected edits, failed search evidence, safe shot description, priority.
7. **Conflicting-feedback queue:** normalized opposing claims, context matrix, decision/performance status, recommended next action.
8. **Weekly learning digest:** template above.
9. **Proposed documentation changes:** reviewable diffs only, never silent writes.
10. **Machine-readable preflight rules:** compiled only from approved lessons and constraints.

Example preflight rule:

```json
{
  "rule_id": "RUL_<26-char-ulid>",
  "lesson_id": "LSN_<26-char-ulid>",
  "status": "approved",
  "severity": "block",
  "scope": {"media_type": "motion_video", "workflows": ["*"]},
  "predicate": "freeze_duration_seconds >= 0.4",
  "exceptions": [{"source_media_type": "intentional_photo_still", "requires_manifest_flag": true}],
  "evidence_feedback_ids": ["FBK_<26-char-ulid>", "FBK_<26-char-ulid>"],
  "approved_by": "content_owner",
  "effective_at": "ISO-8601",
  "review_due_at": "ISO-8601"
}
```

## 10. Integration options and present access

| Source | Automatable now in this environment | Needs additional access/authentication/product work | Manual fallback |
| --- | --- | --- | --- |
| Slack | Connected read/search/channel/thread/reaction tools are available for an interactive import. Existing logs already preserve Slack timestamps. | Unattended continuous ingestion needs a Slack app/event subscription or scheduled authenticated poll, approved scopes, channel allowlist, edit/delete events, retention policy, and durable cursor. Exact permalinks should be resolved during capture. | Paste permalink/message into intake form; attach screenshot/export if private or inaccessible. |
| Codex tasks | The desktop can list and read accessible tasks/turns by task ID. Local job JSONL/session artifacts can be imported now. | Durable background ingestion needs a stable task inventory/event API or bounded polling contract, plus rules for tool output, summaries, user edits, and deleted/archived tasks. | Add task share/ID and exact quoted turn to manual intake. |
| Asana | Connected task/project/search/attachment tools are available; task search covers names, descriptions, and comments. Existing task IDs can be linked. | Complete incremental story/comment history, webhook events, custom-field mapping, and deleted/edit audit may require Asana API OAuth/webhooks and workspace admin approval. | Paste task permalink/comment and task GID. |
| Local Markdown/JSON/JSONL | Fully automatable now with `rg`, parser adapters, file hashes, and a filesystem watcher. Existing `REVIEW_LOG.md`, Frame comment dumps, Codex JSONL, and learning ledgers are immediately ingestible. | Stable anchors require file hash + line-span strategy; Git history is unavailable in this workspace, so source revisions need compiler-side capture unless the directory is placed under version control. | Drop a note into a watched inbox template. |
| Review tools / Frame.io | Existing local `tools/voiceedit/frameio_review.py` and many `frameio_reviews/*.comments.json|md` dumps can be imported now. | Live Frame.io acquisition has previously failed from DNS/token refresh in worker contexts. It needs supported OAuth/token storage, network reachability, project/account mapping, comment edit/delete handling, asset/version IDs, and verified public/internal links. Other review tools need adapters. | Export comments as JSON/CSV/Markdown or paste a review link plus screenshots/timecodes. |
| Manual notes / iMessage / calls | A local structured intake form/CLI and watched folder can operate now; retain original image/audio/text and transcribe as a derived artifact. | Speaker consent, privacy boundary, transcription provider, and retention policy may require decisions/access. | YAML/Markdown intake with required source, reviewer, timestamp, object/version, quote, and attachment. |
| Published performance | Existing winner evidence JSON and `MANSOORS_WINNERS_SYSTEM.md` provide a starting lineage model. Public grid/browser observations can be imported. | Automated Instagram owner metrics, trial reels, 24h/72h/7d/30d snapshots, and lead attribution require an authenticated supported acquisition path; trial reels likely need the provisioned phone. | Scheduled manual snapshot form with screenshot and observed timestamp. |

### Recommended ingestion contract

Every adapter emits the same envelope:

```json
{
  "platform": "slack",
  "source_native_id": "C123:1786931750.182009",
  "canonical_url": null,
  "source_created_at": null,
  "author": {"native_id": null, "display": "Ivan"},
  "raw": {"mime_type": "application/json", "blob_uri": "sha256/...", "sha256": "..."},
  "context_hints": {"task": null, "render_url": "...", "timecode": null},
  "ingestion": {"adapter": "slack_v1", "captured_at": "...", "cursor": "..."}
}
```

Adapters do not create lessons. They only capture evidence and hints.

## 11. Phased implementation plan

### Phase 0 — decisions and data contract

- Confirm authority, source scope, retention/privacy, canonical workflow/ICP vocabulary, and performance definition.
- Freeze v1 schemas and event semantics.
- Define source-independent IDs and dedupe/independence rules.
- Output: approved design, no production mutation.

### Phase 1 — shared PostgreSQL evidence spine

- Add `review_learning` migrations to the Trial Reel Laboratory PostgreSQL database; reuse its object store, audit ledger, permanent-ID allocator, backup, and restore controls.
- Grant the compiler role `SELECT` on required Shared Core views, `INSERT` on compiler-owned event tables, and no create/update/delete authority over Core creative/media tables.
- Import `REVIEW_LOG.md`, `STELLAR.md`, `MISTAKES.md`, `QUALITY.md`, existing learning JSONL, Frame comment dumps, and Codex job artifacts.
- Generate a linkage/ambiguity report; do not auto-resolve uncertain version matches.
- Deliver hard-constraint, candidate, conflict, and missing-context views.

### Phase 2 — connected interactive import

- Add bounded Slack, Codex task, Asana, and Google Drive/Notion metadata adapters using currently available connectors.
- Add manual intake and immutable attachment capture.
- Run read-only backfills for selected channels/projects/date ranges.
- Measure parse accuracy and duplicate-origin handling.

### Phase 3 — revision and approval lineage

- Require render manifests with stable `render_id`, version hash, source asset IDs/in-outs, workflow and ICP.
- Connect feedback -> revision action -> exact decision event.
- Add proposal approval UI/report and documentation base-hash checks.

### Phase 4 — performance validation and experiments

- Join publication IDs to exact approved render hashes.
- Capture 24h/72h/7d/30d metrics and normalized baselines.
- Add controlled hypothesis/variant registry and stale-rule detector.

### Phase 5 — guarded compilation

- Compile approved hard constraints and proven rules to machine-readable preflight JSON.
- Produce documentation patches and regression-test proposals.
- Run in shadow mode first: report what would block, compare with human decisions, tune false positives.
- Only then enable selected blocking gates with owner approval.

### Phase 6 — future skill packaging

- After real pilots validate extraction, linkage, conflict handling, and approval behavior, package the stable workflow as a concise skill with schemas/procedures in references and deterministic scripts where justified.

## 12. First read-only shadow pilot — Lifestyle Copycats, August 16–17

### Pilot objective and safety boundary

Prove capture fidelity, independent-origin deduplication, Core lineage references, ambiguity handling, scoped classification, conflict preservation, and proposal-only documentation output on the August 16–17 Lifestyle Copycat history.

“Read-only shadow” means:

- all Slack, Drive, Markdown, Core, and review-tool access is read-only;
- the pilot may insert immutable `CAP_`, `FBK_`, `INT_`, `ORG_`, `CFL_`, `LSN_`, and `EST_` shadow rows into compiler-owned tables under one `pilot_run_id`;
- it may create `DCP_` rows only with `draft_shadow` status;
- it may not insert `RUL_` rows, emit `PMD_ ... promote`, change Core objects, update documents, write skills, publish, send Slack messages, or activate/block any preflight rule;
- rerunning with the same adapter idempotency keys must produce no duplicate logical captures/events.

Database role: `review_learning_shadow`. It receives `SELECT` on allowlisted Core views and source alias maps; `INSERT` on shadow-eligible compiler tables; no `UPDATE`/`DELETE`; no Core sequence/ID allocation except through the shared typed-ID service for compiler-owned prefixes. Corrections append superseding rows.

### Fixed input scope

Primary dated source:

- `context/copycat/REVIEW_LOG.md`, only the 2026-08-16 and 2026-08-17 sections.

Derived/corroborating sources used for origin grouping, not extra repetition counts:

- `context/copycat/STELLAR.md`
- `context/copycat/MISTAKES.md`
- `context/copycat/QUALITY.md`

Linkage context only:

- the corresponding Core alias maps for Drive IDs, Slack channel/timestamps, Notion page IDs, versions, renders, human reviews, and publications;
- native Slack threads/reactions when read-only access is available;
- immutable Drive metadata/hash records already held by the Core;
- `TRANSLATION.md`, `BROLL_FAVORITES_REPORT.md`, and `MANSOORS_WINNERS_SYSTEM.md` only for scope/context and possible contradiction, never as independent repetitions of the same review.

No later feedback may change what the pilot says was known on August 17. Later documents can be displayed as later corroboration with their own capture time.

### Extraction and linkage sequence

1. Snapshot every input file as a `CAP_` object with bytes, SHA-256, file path, capture time, and line anchors.
2. Split each log entry into atomic `FBK_` events: separate audio, headline, and freeze complaints; separate review comments from delivery/QC/status events.
3. Capture the native Slack source when accessible. Group Slack original plus Markdown copies/paraphrases into one `ORG_` independent origin.
4. Resolve every Drive/Slack/Notion alias against Shared Core records. Link only exact matches to `REV_`, `VER_`, `RND_`, `PUB_`, `SNP_`, `MED_`, `SEG_`, or `AUD_`.
5. When no exact Core row exists, emit an ambiguity/linkage item with aliases and candidates; never create a local version/render/publication.
6. Create machine-draft `INT_` records. Preserve exact quote, requested revision, inferred reason, target, workflow/ICP scope, and interpreter version separately.
7. Create `LSN_` candidates and `EST_` shadow evidence states. Do not promote.
8. Generate the ten outputs below from SQL views/materialized report queries.

### Required outputs and acceptance criteria

1. **Immutable source captures**
   - Manifest of every `CAP_`, native identifier/path, SHA-256, byte length, capture revision, source timestamp, access method, and object-store key.
   - Acceptance: raw bytes round-trip to the same hash; edited/deleted source simulation appends, never overwrites.

2. **Duplicate-origin grouping**
   - Every `FBK_` assigned to an `ORG_`; show originals, mirrors, paraphrases, grouping basis, confidence, and human-review-needed flag.
   - Expected seed cases: the stellar approval copied into `STELLAR.md`; revision/kill lessons copied into `MISTAKES.md` and `QUALITY.md`.
   - Acceptance: copies of one Slack review contribute exactly one independent count.

3. **Version-linkage report**
   - Columns: feedback ID, external Drive/Slack/Notion aliases, Core `REV_`/`VER_`/`RND_` matches, before/after relationship, match method, confidence, and missing Core identity.
   - Explicitly surface multiple “v2” deliveries, the `Dad...` sequence (`170...` -> `1C7...` -> `136...`), the pulled/reposted items, and Drive URLs whose bytes were later overwritten.
   - Acceptance: no filename or “v2” label is treated as identity; exact Core FK or unresolved status only.

4. **Ambiguity queue**
   - One row per unresolved or multi-match link with candidate Core IDs, evidence for/against, risk, and required human decision.
   - Seed ambiguities: exact approval of several delivered v2s, publication status for reviewed copycats, exact timestamp where only approximate time exists, and overwritten Drive-file lineage.
   - Acceptance: uncertain links never leak into promotion counts.

5. **Hard-constraint registry**
   - A shadow projection of already documented constraints, their authority/source, scope, exceptions, current implementation evidence, and proposed Core/preflight linkage.
   - Seed items: wife-face prohibition; no same/near-identical shot within ~5 seconds; no loop/freeze padding; wrong-Dad identity prohibition; Slack identity/delivery restrictions.
   - Acceptance: registry labels these `observed_existing_instruction`; it creates no new active `RUL_` and changes no gate.

6. **Lesson candidates**
   - At minimum: origin evidence for “you stuck with it”; visible work for the dad-quote beat; first-shot duration hypothesis; split freeze/audio/headline candidates from the quality crash; one-off versus workflow-scoped determinations.
   - Each shows evidence origins, Core links, counterevidence, confidence vector, missing evidence, future workflows/ICPs, and next promotion requirement.
   - Acceptance: no candidate is labeled proven solely from wording or documentation copies.

7. **Conflict queue**
   - Include true conflicts and suspected conflicts resolved by scope.
   - Seed scope test: “family payoff beats empty luxury flex” versus the specific request to end one grind-to-life remake with vacation/car lifestyle. Expected result: related tension, probably not a universal contradiction; preserve both and narrow by narrative promise.
   - Acceptance: an empty unresolved queue is allowed only if the report shows evaluated clusters and why they were scope-resolved.

8. **Missing-footage findings**
   - Use typed `INT_` findings linked to requested story roles and Core asset/segment searches; do not create asset records.
   - Expected honest result: no confirmed unavailable footage for the homeless and working revisions because replacements were found. Record the missing audio for `Life's too short to stay` as an audio-availability finding, not footage. Record the 35-second unused-clip risk as a candidate coverage gap only if Core search evidence supports it.
   - Acceptance: “not searched,” “searched and unavailable,” and “available but unsafe/overused” remain distinct.

9. **Weekly learning digest**
   - Generate the existing digest template for the pilot window with evidence-health metrics, rejections, approvals, conflicts, technical issues, missing context, and zero claimed performance validation where `PUB_`/`SNP_` links are absent.
   - Acceptance: every summary item links to `FBK_`/`ORG_` and applicable Core IDs.

10. **Proposed documentation diffs**
    - Draft-shadow diffs for likely affected sections of `MISTAKES.md`, `QUALITY.md`, `STELLAR.md`, or future machine preflight configuration.
    - Each `DCP_` contains target path/heading, base hash, proposed patch, evidence IDs, counterevidence, materiality, and required approver.
    - Acceptance: zero files are modified, zero proposals are implemented, and rerunning the pilot yields the same proposal content hashes.

### Pilot reconciliation report

The run ends with counts for captures, atomic feedback events, origin groups, exact Core links, ambiguous links, lesson classes, conflicts, missing-footage/audio findings, and draft proposals. It must also list excluded items and why—for example delivery status with no feedback content, machine QC without a human review, or later documents that would falsely inflate August evidence.

### Pilot exit gate

The pilot passes only when:

- 100% of raw quotes reproduce exactly from stored capture spans;
- no Shared Core entity is duplicated;
- every Core-looking reference is FK-validated or marked unresolved;
- duplicate documentation does not inflate independent evidence;
- no uncertain link contributes to promotion evidence;
- no `RUL_` or promoting `PMD_` exists for the run;
- no production document, skill, Slack thread, Drive file, Core creative object, or preflight configuration changed;
- a second identical run is logically idempotent;
- a human can trace every digest/proposal statement to raw evidence and Core lineage.

## 13. Existing `tools/learning` prototype disposition

### Safe to reuse after extraction into the new boundary

| Component/idea | Safe reusable part | Constraint |
| --- | --- | --- |
| `ledger.py` | UTC timestamp helper, generated event-ID concept, simple JSONL import reader | Use only as a legacy importer/helper. PostgreSQL and the shared ID service replace JSONL allocation/storage. |
| `revision_hooks.py` | Same-session revision intent and explicit failure when session/asset mapping is absent | Treat outputs as linkage hints. Replace job/Slack strings with Core IDs and typed `REV_` events. Do not let the hook run learning promotion. |
| `skill_harden.py` | Root-cause must differ from the raw note; packet validation concept; coordinator/media boundary assertion; SHA-256 helper | Keep dormant until an approved `RUL_` and `DCP_` exist. It may implement an approved diff later, never decide promotion. |
| `regression_check.py` | Small pure-check function pattern and isolated fixture runner shape | Reimplement against production manifests/media evidence; keep warning/shadow-only until validated. |
| tests | Temporary-directory isolation, “one video must not alter skill,” same-session checks, coordinator-boundary checks | Port to PostgreSQL transactions/containers and Shared Core fixtures. |
| `notion_rules.py` | Human-readable projection idea | Generate an idempotent mirror from canonical PostgreSQL views. Notion must not append or allocate rules. |

### Requires modification

| Component | Required change |
| --- | --- |
| `schema.py` | Replace defect-only schema and four old classes with `CAP_`/`FBK_`/`INT_`/`ORG_`/`CFL_`/`LSN_`/`EST_`/`PMD_`/`RUL_`/`DCP_`; add Core FKs, five lesson classes, scope, evidence independence, contradictions, performance linkage, and unknown reasons. |
| `classify.py` | Remove keyword-based generality and immediate objective promotion. Emit a recommendation plus evidence-state calculation; never an accepted rule. Count `ORG_` groups, not events/files. Apply class-specific thresholds and contradiction gates. |
| `learning_pass.py` | Split capture, interpretation, evidence evaluation, and decision. Stop writing accepted rules/regression stubs from one approved revision. Produce candidates and draft proposals only unless a separate authorized `PMD_` is supplied. |
| candidate/accepted JSON writers | Convert into idempotent PostgreSQL repositories and report exporters. Candidate files may be exports, never canonical records. |
| `revision_hooks.py` | Reference `REV_`, `VER_`, and `RND_`; record before/after through Core lineage. Approval must come from the canonical human review, not a Boolean supplied by a caller. |
| `skill_harden.py` | Require approved `RUL_`, approved `DCP_`, exact target/base hash, approver, implementation receipt, and tests. Remove its ability to create accepted rules or decide `promotion=immediate`. |
| `notion_rules.py` | Upsert by canonical `RUL_`/`DCP_`, display provenance/status, and stop direct append rows. |
| paths/configuration | Replace hard-coded `/home/box` paths with configured environment/host paths and portable Core/object-store clients. |

### Retire

- `ledger.mark_handled`, because it rewrites the append-only ledger.
- `OBJECTIVE_DEFECTS`/`OBJECTIVE_KEYWORDS` as promotion authority.
- `APPLY_FORWARD_HINTS` as a shortcut to promotion.
- `same_issue_count` based only on defect category and skill.
- `write_accepted_rule` and `learning/accepted-rules/*.json` as sources of truth.
- generic `assert_defect_absent:<category>` fixtures, which can “pass” without testing the claimed defect.
- `writer_skill_lessons.append_ivan_lesson` and automatic `IVAN_LEARNED_RULES.md` mutation. It silently converts edits into permanent skill instructions.
- `RULES_LEARNED.md` append operations as canonical state; retain the file only as a legacy import and later generated view.
- caller-supplied `ivan_approved_revision=True` as proof of approval.
- filesystem creation of hardening packets that imply approval before a `PMD_`/`RUL_`/`DCP_` trail exists.

### Migration risks

1. Copies of Slack feedback in `REVIEW_LOG.md`, `MISTAKES.md`, `QUALITY.md`, accepted-rule JSON, and `RULES_LEARNED.md` may be counted as independent evidence.
2. Existing `rev_*` IDs do not follow the shared prefix/ULID contract; preserve them as aliases, allocate new canonical IDs once, and keep an immutable mapping table.
3. Existing records collapse raw feedback, interpretation, proposed rule, approval Boolean, and action into one payload; migration must split them without inventing missing lineage.
4. Multiple records appear to be test/fixture repetitions (including repeated caption-spelling entries). They must not become production evidence.
5. Hard-coded Linux paths may point to stale or absent artifacts on the Mac and can create false “missing source” conclusions.
6. Drive files were sometimes overwritten. URL identity cannot establish render identity without Core byte hashes/version history.
7. “Approved” may mean an original, a revision, a Slack reaction, or merely a default Boolean. Each must be revalidated against a Core `REV_`.
8. Existing rule files may already influence skills. Importing them as candidates while leaving auto-loaded files active would create split authority.
9. Free-text skill/category matching can merge unrelated workflows and ICPs.
10. Legacy timestamps and approximate CT times can be mistaken for exact UTC ordering.
11. Personal data and private review payloads may be copied into new storage without applying the shared Core retention/access policy.
12. A migration retry could allocate new canonical IDs unless alias mapping and import idempotency are committed atomically.

### Regression tests required before anything can block production

#### Identity, ownership, and immutability

- All compiler IDs satisfy the prefix + 26-character Crockford ULID contract.
- Compiler DB role cannot insert/update/delete Core families, versions, renders, publications, reviews, assets, audio, manifests, or snapshots.
- Every linked shared ID passes a real FK; missing IDs create ambiguity, never placeholders.
- Source capture bytes/hash round-trip; source edits/deletions append revisions/tombstones.
- Accepted evidence states, decisions, and rules cannot be mutated; corrections supersede.
- Retry/concurrency tests prove adapter idempotency and no duplicate logical events.

#### Evidence fidelity and independence

- Exact Unicode/punctuation/newline preservation for all August raw comments.
- One message containing three complaints creates three `FBK_` rows sharing one capture/origin.
- Slack original plus three Markdown copies contributes one independent origin.
- Similar but independently authored comments remain separate origins.
- Hash equality alone does not collapse distinct review events; paraphrase detection cannot auto-merge at low confidence.
- Fixture/test data is excluded from production evidence.

#### Linkage and review semantics

- “v2”/filename/Drive URL alone cannot satisfy version linkage.
- Overwritten Drive bytes open ambiguity/incident handling and never mutate `RND_` identity.
- A `REV_ request_changes` followed by `REV_ approve` preserves both and binds each to the correct subject.
- Caller Boolean approval is ignored without Core `REV_` proof.
- Unlinked or ambiguous version/review/publication/snapshot evidence cannot count toward promotion.

#### Classification, conflicts, and promotion

- “Always,” “never,” profanity, capitalization, or reviewer intensity cannot increase replication/generality.
- One subjective comment stays candidate/one-off unless it qualifies as an authorized hard constraint.
- Thresholds count independent `ORG_` groups and distinct Core review chains.
- Unresolved material contradictions block proven-rule promotion.
- Differently scoped preferences can coexist and are not forced into false conflict.
- Performance from source posts cannot be queried as Trial publication support; snapshot type and Core FK enforce separation.
- Missing/unavailable metrics remain different from zero.

#### Proposal and enforcement safety

- Shadow pilot cannot create `RUL_`, promoting `PMD_`, implemented `DCP_`, or active preflight output.
- Documentation proposal generation is deterministic against a base hash and never writes the target file.
- Stale base hashes block later application.
- Notion/Markdown exports are idempotent projections and cannot feed back as independent evidence.
- Preflight remains report-only until an approved rule, validated detector, false-positive/false-negative study, owner activation decision, and rollback test all exist.
- Each detector has positive, negative, boundary, exception, corrupted-input, unavailable-tool, and cross-workflow fixtures; generic fake blockers are forbidden.
- Production shadow comparison demonstrates acceptable precision/recall against human QC before severity may change from `inform` to `warn` or `block`.
- Rollback, database restore, audit-chain verification, and rebuild-from-events tests pass.

The current test asserting immediate promotion for a caption spelling comment must be replaced with a test that creates a candidate/evidence state and requires a separate authorized promotion decision. Existing tests that treat a generated fixture block as proof of detector correctness must also be retired.

## 14. Human approval points

Human action is required for:

- confirming an ambiguous source-to-render/task match;
- declaring who is an authorized hard-constraint issuer;
- converting a candidate/emerging pattern into a proposed rule;
- resolving reviewer conflicts when context/performance does not;
- approving experiment design when publication is involved;
- approving any material permanent-document diff;
- enabling or changing a blocking preflight rule;
- accepting B-roll privacy/identity ratings or exact safe ranges;
- approving new shoot requests that spend time/money;
- publishing content or treating a post as the performance target;
- deprecating/superseding a previously approved rule;
- changing source retention, privacy, or access scope.

Routine capture, parsing, dedupe suggestions, metrics snapshots, clustering, digest generation, and draft proposals can be automated within approved source scopes.

## 15. Decisions needed before implementation

1. **System owner and authority:** Who may issue immediate hard constraints, who approves creative rules, and who breaks ties?
2. **Initial scope:** The first pilot is now fixed to August 16–17 Lifestyle Copycats; decide whether the first post-pilot migration next adds sales-call or scripted-talking-head history.
3. **Canonical schema names/hosting:** Confirm the final Shared Core PostgreSQL schema names and deployment endpoint. The compiler will share that database and will not use SQLite as permanent memory.
4. **Raw-evidence retention:** How long may Slack/Codex/Asana payloads, screenshots, names, and private review media be retained? Who may view them?
5. **Version identity:** Can every future render be required to carry a stable render ID and manifest hash in Slack/Asana/Frame/Drive?
6. **Approval grammar:** Which exact reactions/status changes/text count as approval, revision, rejection, withdrawal, or publication authorization? The recommendation is an explicit receipt contract, not free-text inference.
7. **Reviewer roles:** Are Ivan, Mansoor, Eddie, editors, clients, and machine QC different authorities by domain?
8. **Performance success:** Which metrics matter by workflow—3-second retention, average watch time, completion, shares, saves, comments, follows, leads—and what baseline/horizons define support?
9. **Minimum proof:** Accept the proposed 2-chain emerging / 3-chain proposed thresholds, or choose stricter values by rule class?
10. **Experiment capacity:** How many controlled variants can the calendar support without disrupting normal publishing?
11. **Preflight enforcement:** Which approved rule domains may eventually block delivery automatically, versus warn only?
12. **Existing learning migration:** Preserve current accepted rules as unverified legacy candidates, or grandfather selected rules after a one-time owner audit? Recommendation: import them as `legacy_unverified`, disable their automatic authority, and re-link their evidence before consideration.
13. **Source connections:** Approve initial Slack channels, Asana projects, Codex task set, review-tool projects, and performance accounts for read-only backfill.
14. **Documentation targets:** Name the permanent documents/skills the compiler may propose patches against and the approver for each.

The acceptance test remains deliberately conservative: success is not the number of rules created. It is whether every recommendation traces to immutable evidence and Shared Core lineage, is scoped correctly, preserves contradictions, deduplicates origins, and stops before doctrine or production behavior changes without human approval.
