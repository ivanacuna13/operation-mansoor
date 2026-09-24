# TRY AGAIN × Mansoor — Mirage/Tesseract creativity test

## Delivery

- [Frame.io review — requires existing project access](https://next.frame.io/project/d30a2c87-d14e-4a0e-b53c-a7cd6a2dc0be/view/7ec5350b-33ba-46cf-8e3f-320648484cc0)
- Local master: `Mansoor - Try Again - Mirage Test.mp4` — 1080×1920, H.264, 30 fps, 12.9 seconds.
- Editable source: `Try Again.tsrct`, with native text, footage, effects, animation, and embedded source audio/fonts.
- Original reference: `reference.mp4` — retrieved from the specified @notsaharsh reel; 1918×1080, approximately 12.9 seconds. `reference-original.mp4` is a separately retrieved lower-resolution embed rendition.
- Review filmstrip: `Previews/Encoded-filmstrip.png`, extracted from the actual encoded export.

This was uploaded to the existing Operation Mansoor project, in a new folder named `PRIVATE - Try Again - Mirage Test 2026-09-23`. Existing project members can access it. No public share, invitation, message, social post, or publication was created. The folder itself is not a restricted folder: the API rejected that optional restriction request before upload.

## Concept: One more frame

Doubt constricts Mansoor into a small frame, surrounded by black. A repeated image accumulates into three adjacent attempts as the question asks what one more could do. A huge black brush-style “DO” strikes onto white, reversing the palette for the visual impact. The image then grows into wider windows of actual working and speaking. The payoff gets the brush emphasis “TRIED,” and the last question sits around a quiet walking silhouette. A replay returns to the opening command. This is an interpretation of repetition and effort, not a claim about Mansoor's private feelings or biography. The final execution uses real footage and editable typography throughout; no generated face or generated footage.

## Reference acquisition: solved

Initial web fetch was throttled. Installed yt-dlp 2026.03.17 failed with a login/rate-limit message. A browser-provider attempt reported no available browser. On retry, downloading the official current yt-dlp release (2026.08.19) into this project and running it successfully retrieved the highest selected video/audio formats. Separately, a direct request to the public Instagram embed returned metadata containing a playable video URL; that file also downloaded successfully. The metadata identifies shortcode DPOYgvQE5zr and owner notsaharsh. This required no user-supplied file or new login.

The actual source is landscape, not portrait. The requested output is portrait. Source filmstrips revealed tiny negative-space typography, repeated imagery, and a huge “DO” change. The filmstrip was actually opened and inspected before authoring.

## What Tesseract handled

Installed/pinned CLI: 0.2.0 (91214aa14b4e2bd9c48622ab0419cb7f288b3e48).

The final project has 39 native layers: 17 text layers, 10 footage placements, 11 rectangles, and one audio layer. All visual editing and rendering was done through the installed Tesseract CLI:

- Packaged existing local Mansoor footage and fonts in a portable document.
- Hard cuts and explicit source/time placement.
- Repeated, scaled footage tiles, controlled framing, and black masking rectangles.
- Knewave brush-style emphasis and Barlow supporting type, with fixed glyphs rather than generated lettering.
- Editable entrance/scale keyframes and an expression-driven stepped push-in.
- Native desaturation, Levels, grain, and vignette effects.
- Native MP4 export at the requested vertical resolution.

No Premiere/After Effects compositing or external picture-rendering replacement was used. This test did not exercise every advertised tool, segmentation, arbitrary 3D, or generative-video services. The installed package is an editing/rendering engine, not an AI-video generation service.

## Every outside operation and gap

1. **Reference acquisition:** web requests, the current yt-dlp release, and direct embed metadata parsing. The plugin does not retrieve Instagram media.
2. **Source inspection:** FFmpeg/ffprobe produced source frames/contact sheets and inspected codecs, dimensions, and duration. This exposed what each source actually depicted. The existing shot files were already local edits from prior Mansoor work, not newly supplied camera originals.
3. **Speech timing:** local Parakeet MLX transcription provided word/phrase timestamps. Tesseract has no bundled transcription. The waveform helper used local FFmpeg for diagnostics. Automated transcription is not a listening check.
4. **Font acquisition:** downloaded Knewave and Barlow font files from the official Google Fonts repository and retained OFL license files. Imported fonts are embedded in the native project.
5. **Audio extraction and exact preservation:** FFmpeg copied the original AAC stream out of the reference. The native project contains that audio at unity gain with footage audio muted. After native video export, FFmpeg stream-copied the original reference AAC into the delivered MP4. The CLI does not expose an audio stream-copy export option; relying on its mixed AAC export would re-encode sacred audio. No speech edits, level adjustments, cleanup, added music, or SFX were made.
6. **Final visual/technical QC:** FFmpeg extracted a readable contact sheet from the encoded output, decoded the complete file, and hashed both encoded AAC and decoded PCM. This was necessary because a native filmstrip result was unreliable (below).
7. **Frame.io delivery:** existing local authenticated Frame.io API code uploaded the master and checked transcode completion. The plugin has no cloud upload/review publishing implementation.
8. **Frame.io playback verification:** authenticated API media links were used to fully decode the uploaded original and high-quality processed rendition. Browser UI navigation reached a login page, so browser-player playback was not observed. The review URL remains login-required.

## What broke and how it was corrected

- **Effect IDs:** first commit rejected repeated effect IDs across footage layers. Assigned composition-unique effect IDs. This was an authoring error caught by validation, not a renderer failure.
- **Font identity mismatch:** importing Barlow Condensed SemiBold reported `Barlow Condensed SemiBold/Regular`, but rendering rejected that exact returned selection as missing. Trying typographic `Barlow Condensed/SemiBold` also failed. Barlow Condensed Regular likewise imported but failed to resolve. Barlow Medium initially failed under its returned `Barlow Medium/Regular`; `Barlow/Medium`, using its typographic family/style metadata, rendered. Final supporting text uses that working face. Knewave rendered correctly. Do not assume successful font import proves render-time resolution.
- **Levels units:** the first authored Levels values used 0–1 endpoints, resulting in nearly black footage. Isolated native preview tests established working 0–255 endpoints. Corrected to input black 38, input white 222, output black 0, output white 255, gamma 0.85. This was an incorrect unit assumption; the inspected JSON schema did not explain those units.
- **Grain color:** grain applied after desaturation introduced colored speckles. Added another native desaturation effect after grain and reduced grain amount from 18 to 10. Final footage is monochrome.
- **Framing:** early payoff crops cut too low on Mansoor's face. Repositioned footage upward and verified the encoded result.
- **Native filmstrip discrepancy:** one final-stage native filmstrip omitted text/white graphics despite those graphics being present in the MP4 export. It cannot be treated as the sole acceptance check. The encoded-export filmstrip shows the actual deliverable; no cause for the discrepancy is claimed.
- **Local FFmpeg build:** the default executable lacked `drawtext` when creating labeled source contact sheets. Used plain contact sheets initially and the already-installed ffmpeg-full binary for labeled diagnostics. This is a host-tool issue, not a Tesseract issue.
- **Frame.io folder restriction:** `PATCH .../folders/{id}` with `restricted:true` returned HTTP 422, “Unexpected field: restricted.” No claim of restricted-folder access is made. Delivery uses existing project membership and no public share.

## Audio findings

Parakeet identified the supplied monologue but did not identify a separate repeated “Do.” It detected a short “Then” at the end. These are automated transcript observations; the audio wins, and the complete original stream was preserved instead of reconstructing the seven-line script or cutting its tail. The “DO” graphic lands on the source's question-ending word.

The reference and master have identical extracted AAC hashes and identical decoded PCM hashes:

- AAC SHA-256: `c5c42517452efe60006dbb1a1fd94a402270c5fc5eebc7f81c058d0a4d63ae74`
- PCM SHA-256: `bdb70384a615656b22d90efa242ec6d752afd8f33c9cd8e1b55a586ad2f71619`

This proves unchanged audio content, not a subjective listening assessment. Any sound already baked into the reference remains. The editable project can reproduce the picture and source mix; repeat the recorded stream-copy step when making a new delivery if bit-exact AAC is required.

## Actual review and limits

Inspected source frames, the reference's visual arc, the source waveform, native diagnostic previews, multiple native filmstrips, and the encoded-export filmstrip. Checked full-size “DO” rendering. The final type uses stable native glyphs, with no generated letter morphing. Source and output fully decode; the master is 1080×1920 at 30 fps with 12.9 seconds of video. Frame.io reports `transcoded`; the original and processed remote files fully decode with both audio and video present.

Normal-speed audiovisual listening was not available to this model. I therefore do not claim a completed subjective listening pass or observed playback in the Frame.io web player. Full decode and source-identical audio are the technical evidence. Filmstrip review also cannot prove every perceptual detail of motion at normal speed.

The visual treatment is a restrained graphic interpretation. It does not reproduce the reference's cutout silhouettes or heavily distressed brush texture: the chosen font has brush character but comparatively clean edges. It also relies on previously cut local footage. Those are creative limits of this version, not claimed plugin impossibilities.

## What I would not trust without checking next time

Font selection names returned by import; effect units inferred from bare schemas; filmstrips as a substitute for checking an encoded export; audio identity after mixdown; or a successful upload as proof that browser review playback works. I would not use this run to promise automated segmentation, client-ready generative footage, or effortless cloud handoff.

## Verdict

Tesseract can build this style's native editable cuts, typography, and monochrome treatments. It is useful for supervised production and prototyping. This test does not support calling it an unattended client-delivery system: font resolution, preview/export consistency, exact-audio handoff, and playback review still need deliberate external checks. The final project is editable and the requested MP4 exists on Frame.io; the normal-speed human viewing/listening pass remains the honest review limitation.
