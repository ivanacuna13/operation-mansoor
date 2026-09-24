# Batch vs deliverable contract

## Defaults
| Case | Project shape |
|------|----------------|
| N scripted reels from one shoot | One batch project, shared media/style, N deliverable sequences |
| One long sales call | One recording project, one analysis, selects + one sequence per clip |
| Genius from one long source | One source project, shared analysis, separate deliverable sequences |
| Related copycats | One batch with separate sequences; unrelated campaigns → separate projects |

## Analysis reuse
Do not re-intake/re-transcribe the same source N times. Cache key: `media_sha256 + analysis_model + settings_version`.

## Workers
- One batch director + durable per-reel state
- Editorial workers get bounded excerpts/candidates — not full re-read every revision
- Start: one Astra editor per source group; measure before adding parallel editors
- Parallel **plans** OK; **one writer** per native `.prproj` (Mac integration worker serializes)
- Concurrent native needs: separate projects with ownership OR Premiere Production — never multi-agent write same file

## Independence
Each reel: own QC → upload → review. One blocked reel must not restart completed siblings. Urgent single-reel corrections may jump the queue.

## Queues (separate)
Editorial concurrency ≠ transcription ≠ transfers ≠ native export. One managed native export queue on Mini to start.
