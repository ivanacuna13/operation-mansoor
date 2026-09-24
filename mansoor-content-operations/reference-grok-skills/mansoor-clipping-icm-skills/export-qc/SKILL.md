# Skill — export and QC

## Use when

Validating an assembly and producing the master file.

## Deterministic checks

- 1080x1920 vertical output.
- Progressive, square pixels, frame rate matches source/sequence.
- H.264 `.mp4`; VBR 1-pass approximately 10-12 Mbps.
- AAC 48 kHz stereo 320 kbps.
- Captions burned in.
- Duration and first/last frame match approved in/out.
- File decodes fully and contains both video and audio.

## Human/model review passes

1. Meaning pass: promise, coherence, delivery, truth.
2. Cut pass: listen around every edit; no clipped phonemes, gaps, or stutters.
3. Visual pass: full-screen quality, face visibility, safe zones, headline balance, caption accuracy.
4. Mix pass: voice dominance and music suitability.
5. Final exported-file pass: watch the actual master, not just the timeline.

Any mandatory failure sends the artifact back to the room that owns the defect. QC does not waive rules.

