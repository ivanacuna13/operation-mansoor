# TRY AGAIN — SIGNAL, revision 3

## Concept
An attempt is a signal fighting its way through interference. The opening command assembles from torn ink; doubt folds Mansoor's silhouette back inside itself; one more step crosses an empty pool of light. DO interrupts at architectural scale. The question becomes a moving searchlight over a real phone call, and the payoff stays with actual work rather than an invented victory. The final question hangs between two beams before the command returns as a small unresolved loop. Monochrome grain, static impulses, horizontal displacement and negative flashes connect the beats.

## What actually ran in Tesseract
Tesseract 0.2.0 locally on the Mini authored and rendered the editable composition: native text and imported fonts, footage layers, DO scale keyframes, difference blending, adjustment layers, and custom WGSL effects. Those effects implement fractured ink reveals, physical grain, one-frame static, horizontal image tears, negative flashes, nested silhouette contours, matte compositing, selective monochrome exposure, floor illumination, moving searchlights and procedural volumetric beams. These are editable effects inside the project, not an externally rendered graphics overlay. No After Effects composition or render was used.

The revision was driven by the 387-frame source analysis in SOURCE-FRAME-ANALYSIS.md. It interprets those observed beats; it does not establish which effects the original creator used. Extra signal interference also responds to the user's explicit direction.

## Every external step and gap
1. Source acquisition and audio extraction used yt-dlp/FFmpeg in the earlier reference intake.
2. FFmpeg prepared short source trims, normalized orientation/resolution and encoded mask movies.
3. Apple Vision generated person mattes outside Tesseract. Generic person segmentation lost the walking subject's head and sometimes body. Per-person instance segmentation improved it, but confidence spill required upper-head and upper-left garbage masks and different thresholds inside Tesseract. Work footage had a background sleeve near the head; the upper-left gate suppresses it. This is an external segmentation weakness, not evidence that Tesseract cannot animate.
4. Font files came from official font distributions. Barlow Condensed imports returned metadata but rendered missing-font errors across tested family/style combinations. Supporting type therefore uses working Barlow Medium; Road Rage and Anton render successfully.
5. FFmpeg stream-copied the original AAC into the rendered video. This avoids relying on an editor's audio re-encoding for the sacred-audio requirement.
6. FFprobe, FFmpeg, Python/Pillow supplied complete-decode checks, frame counts, audio hashes and every-frame contact sheets.
7. Frame.io upload and version management use its API outside the plugin. No public share or publishing action was requested or created.
8. Chrome computer-use playback supplies a separate playback check.

Native posterizeTime was tested on the walking plate and matte, then removed while isolating the segmentation artifacts. It is not used in the final revision, and the tests did not establish a Tesseract timing bug. The earlier AE startup troubleshooting produced no usable project and contributes nothing to this render.

## Source integrity
Four moving sources: white-cap desk contemplation; formal walking footage with the original lobby removed; a continuous phone call; and Mansoor at the cafe laptop. No source is reused as a second unrelated scene. The walking image is a spatial metaphor, not a claim that a luxury setting represents hardship. The work shot isolates Mansoor from colleagues. No biography, relationship, success claim or invented dialogue is added. Source trims are recorded in .tesseract-work/rebuild-v3/source-preflight.json.

## Verification and limits
1080 x 1920, H.264, 30 fps, 387 frames, 12.9 seconds. Every rendered frame was reviewed in contact sheets, with changed walking/work intervals rechecked after corrections. All text uses deterministic font glyphs; short intentional interference is followed by stable reading holds. No generative text or generated person is used.

AAC and decoded PCM SHA-256 values both match the original reference exactly. The entire MP4 decodes without error. Local Chrome playback was checked separately; this is not a claim of human audio audition. Remote delivery verification is recorded in .tesseract-work/rebuild-v3/remote-verification.json once upload completes.

The walking extraction remains the least robust component: small edge chatter is possible around the ghutra and feet. It should not be mistaken for perfect rotoscoping. The title face is distressed Road Rage, an interpretation rather than an exact replica of the reference's brush lettering.

## What I would not trust without checking next time
First-pass automatic person isolation; identity or narrative suitability inferred from filenames; font-import success without a render; audio export for bit identity; or sparse filmstrips for one-frame defects. I also would not claim all AE effects are available based on this test.

## Verdict
Tesseract successfully renders the compositing and procedural motion used here. The earlier weak results were not evidence of its creative ceiling. It is useful for this style with deliberate authoring and rigorous review, but this workflow still needed outside matting, media preparation, audio preservation and delivery tools. This test does not justify an unattended client-ready verdict, and creative acceptance belongs to the user.

## Delivery verification
Uploaded as version 3 in the existing private stack. Original and high-quality Frame.io media both fully decoded without errors. The review web page redirects this browser to login, so authenticated review-page playback could not be confirmed; local playback and remote media decoding were confirmed. No access settings changed.

Review: https://next.frame.io/project/d30a2c87-d14e-4a0e-b53c-a7cd6a2dc0be/view/9b552bd4-782b-4480-b014-c8cb0ebcff79
