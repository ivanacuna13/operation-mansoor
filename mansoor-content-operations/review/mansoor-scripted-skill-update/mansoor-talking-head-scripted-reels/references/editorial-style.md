# Editorial procedure

## Wording and source precedence

1. The latest explicit user or timestamped review correction wins.
2. Otherwise, the approved literal script controls spoken wording and every caption character.
3. Speech recognition locates takes and verifies exports. It never supplies caption copy.
4. If no complete recorded take exists for a line, report the exact mismatch. Do not splice inside a word or fabricate a word-perfect claim.

Create one canonical text for the identified reel before cutting. Preserve approved wording, punctuation, numbers, capitalization, contractions, names, and brand terms. Record any explicit reviewer override instead of silently changing the canonical source.

## External microphone synchronization

- Preserve original camera and microphone files unchanged.
- Correlate camera scratch audio with the external recording, then confirm by waveform and listening.
- Verify sync near the beginning, middle, and end. If the offset changes, correct drift before selecting takes.
- Drive picture and external audio from the same source ranges after sync. Never tighten them independently.
- Mute camera scratch audio in every final render and verify the program stream uses the external microphone.

## Candidate ledger and take selection

For every script sentence or natural phrase, record all complete candidate reads with source time ranges. Reject a candidate for any of these:

- a missing, added, substituted, doubled, or reordered word;
- a false start, restart, stumble, repeated lead-in, or disruptive mouth noise;
- eyes away from the camera during the retained delivery;
- a visible read-down before the final phoneme finishes;
- an ending whose last phoneme cannot be isolated cleanly.

Prefer the strongest complete read with direct eye contact and natural energy. Do not choose the shortest take merely because it is easy to trim.

## Boundary construction

For each selected read, mark:

- first phoneme onset;
- final phoneme release;
- visible gaze-down onset;
- safe incoming and outgoing nonspeech handles.

Cut after the complete final phoneme and before gaze-down. Start just before the next onset without retaining a setup pause. At 30 fps, move boundaries on frame edges and keep synchronized audio sample-accurate. Use only a 3-8 ms fade at a true nonspeech edge if needed to prevent a click.

The target assembled gap is about 100 ms. More than 160 ms fails unless the latest user explicitly requests a dramatic pause. Do not retain a pause merely because it is under half a second; the reviewer repeatedly rejected gaps that were visually and audibly minuscule.

For every join:

1. Listen at normal speed while watching.
2. Listen with eyes closed for clipped phonemes, doubled room tone, breath collisions, clicks, and rhythm.
3. Inspect frames immediately before and after the cut for read-downs, blank looks, or double jumps.
4. Measure the residual nonspeech.
5. Retranscribe the surrounding words after assembly.

Repeat the same five checks at every sentence boundary inside a longer selected read. A source segment can contain several sentences; segment continuity does not prove pause-free delivery.

Also scan inside each sentence. A breath, restart, or glance can create a rejected pause even when the transcript engine groups both sides into one sentence. Use the exact voice track at `-32 dB` and fail any measured silence above 180 ms. Punctuation timing and segment boundaries are not substitutes.

VAD, transcript similarity, and energy thresholds only locate candidates. They cannot approve a boundary. Quiet final words need larger manual protection when the detector underestimates their tails.

## Picture-lock rule

Complete the entire speaking edit before captions, headline, crop-ins, grade, or music. The picture lock must include the exact script once and in order, no setup pause, no lingering tail, no visible read-down, and no damaged word. A fresh transcription and the completed per-boundary audit must pass before styling.

## Captions

- Align every canonical word to the fresh picture-lock word timestamps, then divide those timed words into phrases. Never create cue times by dividing the take duration evenly among caption words.
- Concatenated caption text must equal the manifest's concatenated script text after whitespace normalization. Check the actual rendered DOM text too.
- End each caption when the next begins during continuous speech. Do not create blank timing holes when removing filler or retiming a cut.
- Use the locked Inter Bold, sentence-case, 64 px, `-0.08em` treatment in [accepted-style-spec.md](accepted-style-spec.md).
- Avoid all-caps body captions. Preserve exact numbers and punctuation.
- Format the active DM or comment keyword with straight quotes and uppercase, such as `"BLUEPRINT"` or `"LEVERAGE"`.
- Inspect representative short, long, numeric, punctuation, and CTA captions at full size and phone size. Reject awkward one-word orphan lines or text covering the face.

## Headline

Derive the headline from the opening hook. Keep the claim accurate and instantly readable. Start at 64 px. Fit a longer headline by rewrapping to two or three lines and widening the bubble, not by shrinking below the accepted limit.

Place it on or immediately above the forehead or upper hair area. “Above the head” does not mean high in empty background. It must remain clear of the eyes and mouth through the opening and overlapping crop states. Inspect the actual rendered frame at full resolution and 270x480 before final render approval.

The headline is fully visible at frame zero. Do not fade or scale it in from opacity zero.

## Crop-ins, color, and music

- Crop only meaningful claims, proof, mechanisms, or the CTA. Use smooth 1.05-1.09 emphasis and stable framing between beats.
- Check crop starts and returns against jump-cut times so they do not create a second visual glitch.
- Lower highlights, modestly add contrast and saturation, and deepen blacks while retaining skin and clothing detail.
- Use a fitting track from the requested folder. Mansoor music is non-hip-hop and should feel energetic, cinematic, motivational, ambient, or Hans Zimmer-like.
- Balance music before loudness normalization. It must be audible on a phone and never make speech effortful.

## Batch propagation

Treat a review note as both a timestamp and a failure class. Apply the exact timestamp only to that reel, then re-audit the same class across every join and reel in the batch. Do this before uploading the next version; do not wait for the reviewer to repeat the note.
