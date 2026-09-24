# Accepted first-pass specification

These values come from the revisions the user accepted. Use them as the starting state for every Mansoor talking head scripted reel. Change them only when the current footage or an explicit current instruction requires it. Do not repeat an already rejected state and wait for the reviewer to catch it.

## Cut rhythm and eye line

- First audible word begins within 80 ms of the start. Do not leave a half-second opening setup.
- At every sentence or phrase handoff, preserve roughly 40-80 ms after the outgoing phoneme and 20-60 ms before the incoming phoneme. The assembled residual nonspeech target is about 100 ms and the hard maximum is 160 ms.
- Closing room tone is at most 150 ms unless the current user requests an outro hold.
- Cut before the post-line read-down begins. The retained outgoing frames must still show direct camera engagement; the incoming frames must not contain a setup glance.
- Use 3-8 ms audio fades only at true nonspeech edges. Never crossfade through a consonant or vowel.
- Inspect every join. The repeated “minuscule” pauses in Big Team, Duplicate, Systems, Never Sell Alone, and Outdoor Cheat Code proved that sampling joins is inadequate.
- Inspect sentence boundaries that occur inside one selected source range as well. The September 2 batch falsely passed because its audit covered manifest joins but ignored internal sentence pauses.
- Measure the actual rendered voice track and the fresh post-lock transcript. Never copy `speech_start`, `speech_end`, or gap values from a planning manifest into a QC report as though they were measurements.
- Run the exact-audio silence gate at `-32 dB`. The September 2 revisions showed that `-40 dB` room tone can mask visually obvious pauses. Do not trust punctuation-token duration as speech; ASR punctuation can span hundreds of milliseconds of dead air.
- VAD and energy scans are discovery tools. They previously treated a quiet ending such as “you” as silence. Word timestamps, waveform/listening, post-lock transcription, and cut-side frames all have to agree.

## Body captions

For a 1080x1920 composition, start from the accepted treatment:

- Inter Bold / weight 700;
- sentence case, never all-caps body text;
- 64 px type, 1.08 line height, `letter-spacing: -0.08em`;
- centered dark translucent bubble, about 930 px maximum width, with about 68 px composition side padding;
- normally one or two balanced lines in the lower third;
- a subtle 130 ms transform/position settle that is fully legible on its first frame;
- continuous coverage through continuous speech, with one caption ending when the next begins.

Create caption copy by dividing the canonical script. Do not correct, paraphrase, or regenerate it from ASR. The concatenated caption JSON and the actual rendered DOM caption text must equal the canonical picture-lock manifest after whitespace normalization, including punctuation, numbers, brand terms, and contractions. The active CTA keyword must be straight-quoted and uppercase, for example `"BLUEPRINT"`.

Time each canonical word against the fresh post-lock word transcript, then group those timed words into caption phrases. Evenly spreading a phrase across a take is prohibited: it caused captions to visibly lead and lag speech throughout Recognition, Recruiting Cycle, and The Lone Wolf.

## Hook headline

- Use one concise sentence-case headline derived from the hook. It must state the actual promise or tension without inventing a claim.
- Place the bubble on or immediately above Mansoor's forehead or upper hair area. Do not float it high in empty sky or wall space. It must stay clear of the eyes and mouth throughout the opening and any simultaneous crop.
- Default to 64 px Inter Bold with about `-0.065em` tracking and 1.00-1.04 line height. The headline must never be below 56 px or below 87.5% of the 64 px body-caption size. If a longer headline does not fit, rewrap it into two or three balanced lines and widen the bubble; do not shrink it to 46 px.
- For 1080x1920, the accepted long-headline baseline was 64 px, three lines, about 976 px maximum bubble width, about 52 px composition side padding, and about 24/34/28 px bubble padding. Vertical position is subject-relative; the accepted outdoor example used roughly `top: 350px`, while other framing can require a lower top value.
- Show it for roughly the first 4-5 seconds. It must already be fully opaque at timestamp 0.000; only its exit may animate. A blank first frame is a hard failure.
- Inspect a full-resolution opening frame and a 270x480 phone-size frame. Also inspect the headline during every crop state that overlaps it.

## Crop-ins

- Use only on a central claim, concrete number or proof point, mechanism reveal, or CTA.
- A typical accepted emphasis is a smooth move to about 1.05-1.09 scale, often 1.08, with roughly 140 ms in and 160 ms out.
- Keep the image stable between emphasis beats. Do not create rapid decorative zoom alternation.
- Never crop hair, chin, headline, captions, eyes, or mouth. Avoid starting or ending a crop on an unrelated jump cut.

## Grade

- Lower highlights, add modest contrast and saturation, and deepen blacks slightly.
- Protect skin tone, white clothing texture, and background detail. Check early, middle, and late frames; do not grade from one frame.

## Music and final mix

- Use the requested music folder. Reject hip-hop for Mansoor.
- Prefer energetic cinematic, motivational, ambient, or Hans Zimmer-like tension. A sad low-energy choice was rejected.
- Music must be audible on a phone but never compete with speech. Check speakers and a phone; every consonant must remain effortless to understand.
- Treat gain values as track-specific. Measure dialogue-to-music level and listen. A useful starting range is roughly 14-22 dB of dialogue advantage.
- Target about -14 LUFS integrated and no higher than -1 dBTP; the accepted masters were around -14.2 LUFS and -1.5 dBTP.
- Use short music fades at the reel edges. Do not use final loudness normalization as a substitute for balancing voice and music first.

## Failure history converted to rules

| Repeated review failure | First-pass rule |
|---|---|
| Tiny pauses after nearly every line | Measure the final voice track and fresh transcript at every sentence boundary, including boundaries inside a manifest segment; target 100 ms and fail above 160 ms. |
| Glitchy or double jump cuts | Inspect cut-side frames and listen through every join; one clean visual discontinuity only. |
| Words cut off while tightening | Preserve complete phonemes and re-diff a fresh picture-lock transcript. |
| Mansoor looks down after a line | End before the gaze drop, not after the silence. |
| Caption spelling or wording errors despite a script | Script-to-JSON-to-DOM equality is mandatory. |
| CTA capitalization errors | Use the exact straight-quoted uppercase keyword. |
| Headline too high | Align to forehead or upper hair, not empty negative space. |
| Long headline shrunk to 46 px | Rewrap or widen; keep at least 56 px and preferably 64 px. |
| Music sad, hip-hop, too quiet, or too loud | Use energetic non-hip-hop music and complete a phone speech/music check. |
| One note fixed while the same defect remained elsewhere | Propagate every failure class across every join and reel before delivery. |
| QC booleans marked true without evidence | Reject the audit. Values must be derived from the exact final render or backed by named visual/listening evidence. |
