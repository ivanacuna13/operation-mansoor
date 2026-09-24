# Frame-sourced edit rules (Sales Call 04 / 05 / 06)

Only rules with on-disk Frame comment dumps or job QC verification. Do not invent timestamps.

## Sources on disk

| Clip | Review kind | Path |
| --- | --- | --- |
| Sales Call 04 | clip | `/home/box/mansoor-content-operations/jobs/import:sales-call-04-felony:v1/workspace/output/frameio_reviews/clip.comments.md` |
| Sales Call 04 | revision_final | `.../import:sales-call-04-felony:v1/workspace/output/frameio_reviews/revision_final.comments.md` |
| Sales Call 04 | QC verify | `.../import:sales-call-04-felony:v1/workspace/qc/revision-v5/QC-REPORT.md` |
| Sales Call 05 | clip | `.../import:sales-call-05-twenty:v1/workspace/output/frameio_reviews/clip.comments.md` |
| Sales Call 05 | revision_final | `.../import:sales-call-05-twenty:v1/workspace/output/frameio_reviews/revision_final.comments.md` |
| Sales Call 05 | QC verify | `.../import:sales-call-05-twenty:v1/workspace/qc/v4-manual-qc.json` |
| Sales Call 06 | clip | `.../import:sales-call-06-policy:v1/workspace/output/frameio_reviews/clip.comments.md` |
| Sales Call 06 | revision_final | `.../import:sales-call-06-policy:v1/workspace/output/frameio_reviews/revision_final.comments.md` |
| Specs | project | each job `workspace/sales-call-spec.json` |

## Hard rules extracted from Frame text

### Opening

1. **No frames before the opening headline.** Frame: “No frames should exist in beginning without headline” / “No frames should exist without headline in the beginning” (SC04 clip @00:00:00.000; SC06 clip @00:00:00.000).
2. **Opening must be moving video, not a still.** Frame: “Why is this frame not moving where is the video” (SC05 clip @00:00:03.333).
3. **Open with Mansoor centered.** Frame: “never start with footage that doesnt have him in center of frame” and “start video here” (SC05 revision_final @00:00:01.667 / @00:00:09.933). Also “Center his head” / “Center him” (SC05 clip @00:00:15.900 / @00:00:24.567).

### Opening headline geometry

4. **Headline must not sit too high or too small.** Frame: “The headline is way too small and way too high” (SC05 clip @00:00:05.000); “Headline is way too high” (SC06 clip @00:00:00.867); “headline is way too high bring it down a bit” (SC06 revision_final @00:00:00.700). Keep the approved forehead relationship from `visual-spec.md`.

### Captions

5. **One line, about 4–5 words; readable size.** Frame: “Captions too small and too many words on one line. Limit to one line maybe 4-5 words at a time.” (SC04 clip @00:00:07.400); “Cations should be limited to one line and only 4-5 words per line. They’re too small to read” (SC06 clip @00:00:00.867).
6. **Captions must stay centered.** Frame: “Uncentered captions grave violation” (SC06 clip @00:00:22.167).
7. **Never crop the caption off.** Frame: “caption shoul dnever be cut off. you shouldnt be croppping in on both the photoage and the caption” (SC06 revision_final @00:00:10.167). Phone close-up must not push captions out of frame.
8. **Every audible stretch needs captions.** Frame: “captions not entered at all” (SC06 revision_final @00:00:37.167); “bad caption” (same timestamp cluster).
9. **Do not cut off words.** Frame: “You cut off his words” (SC06 clip @00:00:06.367).

### Cuts, pauses, flash frames

10. **Cut avoidable pauses.** Frame: “Cut pause out” / “Cut out pause” (SC04 clip @00:00:27.967 / @00:00:43.667; SC06 revision_final @00:01:18.800).
11. **No flashing / lagging half-second leftover frames at joins.** Frame: “unclean cut. you have a flashing half second frame left in the cut” (SC04 revision_final @00:00:42.567); “you have a flashing frame thats left over from the cut. stays for liek half a second and is jarring” (SC05 revision_final @00:00:23.800); “lagging frame unclean cut” / “dont have lagging frame or glitchy cut” (SC06 revision_final @00:01:01.633 / @00:01:18.800); “Super glitchy and unclean cut” (SC04 clip @00:00:44.667). Positive exemplar: “example of a clean cut with no lagging or flashing frames” (SC05 revision_final @00:00:15.700).

### Client crop / speaker ID

12. **Crop in at the first client phoneme, not mid-word.** Frame: “The crop in happened to late when the speaker was mid word” (SC04 clip @00:00:29.100).
13. **Do not oscillate crop during a pause inside one client turn — keep the close-up and cut the pause.** Frame: “No need to cut out and in during a pause. Just keep it on the crop in and cut out the pause” (SC04 clip @00:00:30.100).
14. **Speaker attribution must be correct.** Frame: “Mansoor says “even on the probation” not the client” (SC04 clip @00:00:35.833); “this part the client is talking not mansoor” (SC06 revision_final @00:01:22.567).

### Story arc / ending

15. **Do not end before the payoff / climax.** Frame: “This didn’t come to a clean ending. Needs to have some kind of pay off. This just ended mid convo” (SC04 clip @00:00:46.700); “You cut off this video way way too early. This was peak climax as he is handling the objection/conflict. You ended it right at the best part” (SC06 clip @00:00:33.167). Positive exemplar: conflict → payoff that “Makes sense on its own and feels complete” (SC05 clip @00:00:52.500).
16. **End with a short concluding headline that states the point / resolution.** Frame:
    - SC04 revision_final @00:00:47.133: “end video here. end video by having a 5-10 second second headline that provides context to how the call is resolved aka the "point" of the video … one short sentence is enough. like this one is "this iswhy you don't give up on your clients"”
    - SC05 revision_final @00:00:51.667: “end video with a 7 second headline explaining resolution of the video "Another family protected ✅ "”
    - SC06 revision_final @00:01:26.400: “end the video with a new headline "client successfully redirected into buying conversation" helps tell story and provide context as to what the point ofthe video was”
17. **Verified implementations (not invented):**
    - SC04 v5 QC: six-second contextual card “This is why you don’t give up on your clients.” (`QC-REPORT.md`)
    - SC05 v4 QC: `resolution_headline_duration_seconds: 7.0`, text “Another family protected ✅” (`v4-manual-qc.json`, `sales-call-spec.json`)
    - SC06 `sales-call-spec.json` approved deviation notes a **~1.867–1.9-second** closing story card at 85.800s — **approve-path outlier**. Skill soft-default remains **~7 s** (SC05); do not block waiting on Ivan for a duration decision.

## Slack digests

Job `slack-revision-reply.json` files exist for SC04/05/06 but only record **blocked** bot sends (`status: blocked_before_bot_send`). They contain no additional editing doctrine beyond Frame upload links. No Slack revision-thread digests with Frame-note paraphrases were found under these jobs.
