# Mansoor short-form style specification

## Canvas and image

- Deliverable: vertical 1080x1920.
- Use full-screen talking head when source resolution supports it.
- Preserve source/sequence frame rate; the tutorial example is 23.976 fps.
- Keep key face and text elements out of Instagram/platform red zones.

## Text headline

- Function: visual hook for roughly the first four seconds.
- Content: promise or curiosity gap that complements the verbal hook.
- Maximum: two lines.
- Alignment: dead center.
- Placement: around/below the chin, legible, balanced, not top- or bottom-heavy.
- Typeface: Manrope Bold in the demonstrated example.
- Treatment shown: black text on a white background block, with size adjusted to fit the approved phrase.
- Do not run standard captions beneath the headline during its opening display.

## Captions

- Typeface: Manrope Regular.
- Font size: 23 in the demonstrated Premiere sequence.
- Tracking: -27.
- Position: centered; Premiere caption position shown as 70 units down.
- Color: white.
- Shadow: very slight. Exact numeric shadow values are not legible in the supplied evidence; match the visual reference, do not invent a canonical number.
- Maximum characters: 23.
- Minimum caption duration: 2 seconds.
- Lines: exactly one. Double lines are forbidden.
- Placement: directly below the mouth/around the chin, never covering the mouth or face, and clear of red zones.
- Copy: verify every word and punctuation mark against the engineered audio.

## Audio

- Spoken voice is primary, shown around -1 to -3 dB while speaking.
- Music is optional; silence is preferable to an unhelpful bed.
- If used, choose instrumental music that fits the emotion and does not overpower the voice.
- Flat music in the example sits roughly -18 to -20 dB. Dynamic tracks require automation/ducking rather than blind reuse of one number.

## Export

- Format: H.264 `.mp4`.
- Frame: 1080x1920, progressive, square pixels, source/sequence frame rate.
- Render at maximum depth: on.
- Use maximum render quality: on.
- Performance: hardware encoding when available.
- Bitrate: VBR, 1 pass, target 10-12 Mbps; screenshot example is approximately 11.7 Mbps.
- Audio: AAC, 48 kHz, stereo, 320 kbps.
- Captions: burn into video.
- Range: source in/out.
- Color: match source and sequence. The tutorial example displays an HDR/P3 output; do not force that profile onto SDR footage.

