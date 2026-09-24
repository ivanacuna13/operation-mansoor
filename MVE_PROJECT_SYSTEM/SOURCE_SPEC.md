# Prompt for Grok Bot: Mansoor editing projects, version control, and batches

Implement this across Master Video Editor's Mansoor editing operation. Do not limit it to scripted talking heads. The goal is fewer first-review technical defects, faster batch turnaround, recoverable projects, and reliable revisions.

## 1. Inventory the actual routes first

Inspect the live Master Video Editor registry, dispatcher prompts, installed SKILL.md files, their dependencies, revision handlers, render workers, and delivery paths. Report the exact registered formats and skill paths. A historical registry contained:

- sales_call_clip → mansoor-sales-call-clips
- scripted_talking_head → mansoor-talking-head-scripted-reels
- genius_clip → mansoor-genius-clips
- lifestyle_copycat → mansoor-tof-copycat-editor

Verify these against the current machine and include any added/renamed routes. Do not confuse a registered path with an installed or working skill. Preserve each format's editorial doctrine and delivery destination. Apply the shared project/version/QC rules below across every route. Do not convert an unscripted call into literal scripted content, or replace an audio-preserving overlay request with a new script.

## 2. Make project-based editing the common foundation

An editor revises the editable source project, not a previous exported review movie.

- Keep original camera/audio/reference files immutable, with stable IDs, paths, hashes, frame rates, timebases, durations, and channel maps.
- Keep proxies, analysis audio, renders, captions, graphics, and caches clearly distinguished from originals.
- Maintain source-to-timeline mappings for every deliverable. Preserve source timecode where present and source frame indexes in all cases.
- Revisions must edit the versioned source timeline, source-linked Premiere sequence, and supporting assets. Never substitute the previous review MP4 for the original camera recording.
- Recover missing originals or mapping before destructive editorial repairs; return a precise blocker if recovery fails. A finished reference video is legitimate as a reference or intentional insert, not a substitute for missing edit sources.
- Use explicit frame-based picture boundaries and sample/time-based audio positions, accounting for variable-frame-rate material and timecode offsets. Preserve sync, handles, transitions, effects, and channel layout.

Use manifests and Premiere-compatible XML to assemble source-linked timelines. Once conformed in Premiere, preserve the native project as the editable master. Keep the manifest, XML, native project, and export tied to one revision ID. XML is an interchange representation, not a lossless substitute for every native Premiere feature.

If a native edit cannot round-trip through XML faithfully, retain it in the native master and apply subsequent changes through Premiere's scripting interface. Record what is native-only. Do not regenerate a simplified XML project over a finished native edit and lose its effects, graphics, audio, or captions.

## 3. Adopt professional project organization and immutable milestones

Use a predictable structure, adapted to the current storage system:

```text
BATCH_OR_RECORDING_ID/
  00_admin/          brief, source inventory, deliverable roster
  01_originals/      original media or controlled references to shared originals
  02_proxies/        rebuildable proxies and analysis audio
  03_analysis/       untouched ASR, candidates, source notes
  04_projects/       versioned native projects, manifests, interchange XML
  05_assets/         versioned captions, graphics, music, SFX
  06_qc/             evidence tied to exact revision and render hash
  07_exports/        versioned masters and review files
  08_delivery/       Frame.io IDs, comments, upload/playback receipts
  09_archive/        archival manifests and restore instructions
```

Create named bins and stable sequence IDs for source recordings, selects, working cuts, and deliverables. A selects/stringout sequence is useful for discovery, but each independently reviewed deliverable gets its own export sequence.

Example naming:

```text
MAN_BATCH_20260908_project_r003.prproj
MAN_CALL_004_CLIP_006_edit_r004.json
MAN_CALL_004_CLIP_006_9x16_review_r004.mp4
```

Separate project revisions, per-deliverable revisions, and export preset variants. Use stable IDs, not titles alone. Mark approval in metadata against an exact asset/revision rather than repeatedly renaming files FINAL.

- Before a material change, save an immutable project checkpoint. Ordinary working saves may update the designated working copy, but never overwrite delivered/approved milestones.
- Version referenced graphics and captions too. An old project must not silently change because a PNG at a shared path was overwritten.
- Store parent revision, timestamp, editor/model, source/asset hashes, sequence IDs, and exact change list.
- Log each change with comment ID where applicable, old/new timeline and source ranges, rationale, and affected QC checks.
- Keep an append-only delivery history and an explicit current-working/current-approved pointer.
- Preserve rejected versions and comments unless a separate retention decision authorizes removal.
- Enable autosave, but do not treat autosave as the backup plan. Back up originals and immutable project/assets to an independent location and perform a restore/relink test. Cache cleanup must never delete unique media or approved milestones.
- Write outputs to temporary names, verify completion, then promote them. Retry delivery without creating a new editorial revision or duplicate upload.

## 4. Astra edits; the system executes and tracks

Verify the available Astra model identifier and use it for initial editorial decisions and substantive revisions. Record actual model/effort used. No silent downgrade or substitution.

Grok Bot owns intake, dispatch, queue, state, and blocked-work visibility. Astra chooses takes, arcs, source ranges, and visual/audio treatment. Deterministic tools prepare, assemble, render, measure, and deliver. Keep expensive model reasoning out of routine polling and file bookkeeping.

Shared doctrine: prefer the best complete performance over many repairs to a weak take. Silence detection and ASR timestamps flag candidates; they do not independently establish safe phoneme boundaries or visual continuity.

Retain format-specific requirements:

- Scripted: compare complete repeated takes, preserve approved intent/wording constraints, direct eye contact, and coherent delivery.
- Sales calls: preserve conversational context, speaker roles, truthful chronology/meaning, privacy requirements, and payoff. Analyze the recording once, then select several distinct clips.
- Genius clips: inspect the installed skill's actual selection criteria. Analyze the long source once; identify complete standalone arcs and avoid unnecessary duplication between deliverables.
- Copycats: preserve the reference's intended structure/style while using authorized source material; keep clip-specific reference mapping and prevent unintended audio replacement. Verify the actual skill rather than assuming every copycat has identical needs.

## 5. Batch related work, isolate deliverables

Default organization:

- Ten scripted reels from one shoot: one batch project, shared media/style bins, ten named deliverable sequences, ten outputs.
- One hour-long sales call: one recording project, one transcript and speaker analysis, a selects sequence, one sequence per selected clip, multiple outputs.
- Genius clips from one source: one source project, shared transcript/candidate analysis, separate deliverable sequences.
- Related copycats from a common shoot/style: one batch with separate sequences. Unrelated sources, styles, or campaigns may warrant separate projects rather than one oversized project.

Do not create ten independent intake/transcription runs for the same source. Cache by media hash plus analysis model/settings version. Load shared brief/style/context once and persist per-deliverable checkpoints.

One project is not synonymous with one enormous model conversation. Use one batch director and durable per-reel state; give editorial workers bounded source excerpts/candidate data. Start with one Astra editor per source group, and allow a small measured number of independent editorial workers for different deliverables/groups. Do not reread every full transcript on every revision.

Workers may prepare independent edit plans in parallel. Only one owner may write a particular native project at a time. A dedicated Mac integration worker serially applies validated plans and saves checkpoints. If genuine concurrent native editing is needed, use separate projects with explicit ownership or an appropriately configured Premiere Production; multiple agents must not write the same .prproj concurrently.

Each reel can pass QC, upload, and enter review independently. One blocked reel must not hold the whole batch or restart completed work. Urgent single-reel corrections may be prioritized in the queue.

## 6. Use Premiere and Media Encoder where they provide value

On the Mac mini, use a supported Premiere scripting bridge in a logged-in desktop session to import/conform, verify links and sequence settings, save native project revisions, and queue exports. SSH transfers/submits jobs; it does not turn Premiere into a headless Linux service.

Use Media Encoder for queued native sequence exports and required output variants. Freeze the exact export revision: queue from an immutable project/sequence snapshot, and do not mutate assets underneath a queued job.

Keep editorial concurrency separate from CPU transcription, transfers, and exports. Start with one managed native export queue on one Mac; benchmark before increasing heavy-render concurrency. Do not launch ten competing Premiere/FFmpeg render processes merely because there are ten clips.

Do not promise Premiere/AME is always faster than FFmpeg. Benchmark the actual mini, footage codec, effects, captions, hardware-encoding settings, quality target, and storage. Use FFmpeg for suitable proxies, measurements, or faithful preview renders; use native exports when native rendering fidelity matters. Maintain consistent frame counts, timings, audio, color, and graphics between review and final.

## 7. Repair QC and revision identity

Remove automatically asserted listening/word-integrity/visual-pass flags. Never clamp measurements to passing limits. Keep untouched ASR separate from editorially corrected text. A valid XML, successful decode, completed process, or uploaded file is not proof of clean cuts.

Before my first review:

1. Assemble a lightweight source-linked cut.
2. Inspect actual joins, suspicious internal pauses, clipped phonemes, eye contact, and visual discontinuities.
3. Replace bad takes or adjust source ranges.
4. Lock picture timing, then generate/update captions.
5. Inspect the actual finished export and record evidence against its hash.

Flag tiny fragments/clustered cuts for inspection without blindly deleting valid short moments. Preserve true measured results. Separate automated evidence from subjective review. An independent reviewer pass must not approve solely by rereading the editor's pass flags.

Classify revisions by affected layer: source/timing, captions, graphics, sound, or delivery. Run affected checks plus proportionate regression checks. A graphics-only revision must preserve approved source ranges and audio; an upload retry must not rerender.

Resolve the actual latest Frame.io stack head before reading comments and again before upload. Bind the job to asset ID, comment IDs, sequence ID, project revision, and render hash. Detect newer revisions, conflicting ownership, and duplicate filenames. Map reviewed timestamps through that reviewed revision to original sources. Preserve one stable review stack/link per deliverable and old comments.

Distinguish process success, media readiness, upload completion, playback readiness, delivery completion, and approval. A blocked worker cannot become Edit Ready for Review merely because it returned text or exited cleanly.

## 8. Verify the implementation, then scale

Implement common project/version/ownership/queue/QC contracts once and connect all registered format skills. Keep creative rules in the appropriate skills. Do not merely append another long instruction document while leaving unsafe code in use.

Demonstrate with representative real jobs: a scripted batch, multiple clips from one sales call, and available Genius/copycat work. Test source-level and graphics-only revisions, restore of an older version including its assets, interrupted export recovery, duplicate-upload prevention, and a newer Frame.io head arriving mid-job.

Measure cold-start and cached runs separately. Compare equivalent output quality and QC scope. Record total batch turnaround, time to first ready clip, transcription/analysis reuse, Astra usage, render time, memory/storage pressure, first-review technical defects, and human correction rounds. Separate styling preferences from technical defects.

Start with a small pilot before a ten-deliverable batch. Report exact changes, verified skill coverage, measured results, remaining blockers, and what is still only proposed. Do not rewrite existing approved edits or publish unsolicited replacements while implementing the infrastructure.
