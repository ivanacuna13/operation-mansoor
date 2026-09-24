# TRY AGAIN × Mansoor — rebuilt v2

## Status and files

[Frame.io rebuilt revision](https://next.frame.io/project/d30a2c87-d14e-4a0e-b53c-a7cd6a2dc0be/view/01532436-59f6-40cd-9e72-7aac6bf6ecf7) — login and existing Operation Mansoor project access required. V2 is uploaded in the original private-test folder and grouped with rejected v1 in a version stack. No public share, invitation, social post, or message was created. The folder inherits existing project access; its name is not a security restriction.

- Master: `Mansoor - Try Again - Rebuilt.mp4`, 1080×1920, 30 fps, 387 frames, 12.9 seconds.
- Native editable project: `Try Again - Rebuilt.tsrct`.
- Reference analysis: `SOURCE-FRAME-ANALYSIS.md`.
- Full source review: `Previews/source-every-frame/`, all 387 original frames.
- Full output review: `Previews/rebuilt-every-frame/`, all 387 exported frames.
- Exact source IDs, intervals, identity observations, story roles and exclusions: `.tesseract-work/rebuild-v2/preflight.json`.
- Reproducible native authoring: `.tesseract-work/rebuild-v2/build_v2.py`.
- Rejected v1 and its original log: `Versions/Rejected v1 - …`.

## Accountability for v1

The original delivery failed. I did not do a complete source-frame analysis or apply Mansoor’s existing B-roll rules before selecting footage. It included a specifically prohibited wrong-person clip, reused sources, weak framing and superficial typography. Those were my research, selection and craft failures. They are not plugin limitations. The old review is not approved, and the preserved v1 log must not be read as a current quality endorsement.

## Concept: the next attempt

A distressed command appears in two strokes. Mansoor at his desk is isolated in black; outlines accumulate beneath and within his body as doubt turns inward. A real writing action occupies a constrained pool of light. The giant DO interrupts that small world and reveals moving phone-call footage through the letters. The image opens into active participation, then a present-day office conversation: the payoff is showing up, without claiming a sale, achievement or private emotion. The final question stays legible while the light withdraws to a narrow mark. The progression is an editorial interpretation of persistence, not a biographical timeline. No unrelated people, luxury-as-hardship, invented relationships or duplicate source cuts are used.

## What Tesseract actually handled

Official installed plugin CLI 0.2.0, not a substitute renderer. The new native document contains 29 layers: {'Text': 17, 'Rect': 6, 'Video': 5, 'Audio': 1}. The central graphics and final picture render are Tesseract-native:

- Native text with embedded Rubik Dirt, Anton and Barlow fonts. Stable glyphs, not generated text.
- Short brush-like reveal shaders over distressed type, editable position/scale keys, and staged phrase entrances.
- The native video/mask texture binding and custom WGSL shader that extracts the desk subject, generates nested contours and animates their accumulation.
- Native oval spotlight, exposure sweep and a configured `posterizeTime` effect for the effort beat.
- Difference-blended giant DO over continuous moving footage, followed by a one-frame negative punch.
- Native monochrome grading, moving light/exposure, grain and darkened text-safe image regions.
- Native white flash punctuation, hard cuts, and final procedural light withdrawal.
- Video timing, muted footage, the original audio layer at unity, and 1080×1920 MP4 export.

This is not a claim of mastering all advertised tools. The local package has no bundled Instagram retrieval, transcription, generation or Frame.io upload workflow.

## Every outside operation and gap

1. **Reference retrieval:** official yt-dlp and Instagram embed metadata retrieval, outside the plugin. The exact reel was recovered; no replacement audio was invented.
2. **Reference and footage inspection:** FFmpeg/ffprobe generated complete sequential reference/output frame sheets, selected-range sheets and full-resolution frames. I opened all 387 source frames and all 387 final frames, rather than extrapolating from sparse thumbnails.
3. **Source retrieval:** reused local camera sources and downloaded original desk, Zoom and profile files via their cataloged Drive IDs. The profile file was inspected and rejected. Catalog labels were treated as leads, not identity proof.
4. **Speech timing:** the retained local Parakeet transcript and waveform informed timing. Automated transcription is not a listening pass; the audio, including its tail, was retained unchanged.
5. **Fonts:** downloaded official Google Fonts files and licenses. The fonts are embedded in the project. Rubik Dirt replaced the clean, cartoonish-feeling first title treatment.
6. **Person segmentation:** Tesseract’s `personMatte` with `emptyFallback: hide` produced an empty preview in this runtime. A functioning native segmentation resource was not established. macOS Vision produced a real moving person mask; this was encoded and imported. Tesseract performed the mask-based compositing, outline creation and motion. The native shader suppresses an unrelated background region picked up by Vision.
7. **Rejected segmentation experiment:** also tested a Zoom person mask. The source’s hat met the original frame edge, and isolation exposed an ugly straight cutoff and detached mask fragments. That treatment was rejected; its mask is not used in the final timeline.
8. **One source framing fallback:** FFmpeg prepared the Zoom interval at 160.000–161.800s with `crop=1220:1080:700:0,scale=1080:956,pad=1080:1920:0:420`. This keeps the writing hand and profile and excludes the private laptop screen. Native Tesseract applies the lighting, temporal effect, grade and edit. This was a practical fallback after repeated framing-coordinate errors, not proof that the plugin cannot crop.
9. **Sacred audio:** FFmpeg stream-copied original AAC into the native video export, avoiding the plugin exporter’s audio re-encode. No cleanup, gain, timing, word, music or SFX changes. Both encoded AAC and decoded PCM match the reference exactly.
10. **Encoded-output QC:** FFmpeg performed full decoding, frame counting, dimensions/fps validation, and audio hashing. Sequential sheets came from the actual delivered MP4.
11. **Frame.io:** authenticated existing API tooling uploaded the master and created a version stack. This capability is outside Tesseract. No public review share was created.
12. **Playback-check limitation:** native Chrome opened the local MP4 window, but the computer-use provider returned stale accessibility data and “Screenshot unavailable.” The Frame.io browser session was at login. I cannot claim an observed web-player playback or a human audiovisual listening pass. Remote full decoding is recorded separately in `.tesseract-work/rebuild-v2/remote-verification.json`.

## What broke, and attribution

- Native person-matte output was empty; external Vision mask was required for the retained silhouette treatment. Missing model availability is suspected, not proven.
- Early landscape framing used the wrong interpretation of `sourceRect` and transform anchors. The inspected schema gave types without enough coordinate semantics. Explicit display bounds corrected the call. The Zoom shot received the documented external framing preparation. These were authoring/workflow errors; no unsupported claim of a renderer defect is made.
- A crop-derived first desk mask created artificial straight silhouette edges. Rebuilt the mask from the wider original and reframed in the native shader.
- The Zoom isolation attempt failed visual QC despite successful segmentation execution. It was rejected, not disguised as a successful effect.
- An intermediate encoded pass omitted the opening graphics; subsequent encoded passes displayed them. The cause was not established. Together with v1’s preview/export inconsistency, this means the actual MP4 must be inspected after every render.
- Early white captions crossed a bright shirt. Native grading now darkens the caption region without covering Mansoor’s face.
- The initial DO scale used the wrong anchor and clipped the main hold. Centered the anchor; the final stable word is fully visible. Its last frame expands into the cut as intentional motion, after the readable hold.
- V1 font resolution and Levels-unit problems remain documented in its archived log. They were not segmentation or selection excuses.

## Verification and limits

The master has 387 frames at 30 fps, 1080×1920, 12.9 seconds, and decodes in full. Every final frame was opened in sequential labeled sheets, with additional full-size checks of title, silhouette, framing, DO and caption contrast. Each footage beat shows cataloged and visually checked Mansoor; there are four distinct original sources, each used once continuously. The mask is a compositing input for the same beat, not a repeated later shot. The office reaction excerpt ends before another attendee enters.

The title, TRIED and FAIL have brief three-frame reveals followed by settled holds. No AI-generated or morphing glyphs are used. Two-frame white burns and the one-frame negative image are intentional, not corrupt frames. Technical and sequential-frame checks do not replace normal-speed human audiovisual review. That review remains incomplete because the available player UI could not be observed. This revision is for review, not represented as client-approved.

Audio identity:

- AAC SHA-256: `c5c42517452efe60006dbb1a1fd94a402270c5fc5eebc7f81c058d0a4d63ae74`
- PCM SHA-256: `bdb70384a615656b22d90efa242ec6d752afd8f33c9cd8e1b55a586ad2f71619`

## What I would not trust next time

Catalog descriptions without opening the footage; any previous agent’s person identification; source repetition disguised as another in/out; native segmentation without a real mask test; coordinate assumptions for mixed-aspect footage; a successful export without opening the encoded frames; or a successful upload as proof of observable web-player playback. The first three are editorial controls that I failed, not plugin gaps.

## Verdict

Tesseract is capable of substantially more than the first delivery demonstrated: editable distressed typography, real-mask contour compositing, footage-through-type, procedural light and native motion are feasible. This test supports supervised motion-design work with external source/matte preparation and rigorous output inspection. It does not support unattended client delivery. The visual decisions still require an editor, and the normal-speed audiovisual review remains an explicit open check.
