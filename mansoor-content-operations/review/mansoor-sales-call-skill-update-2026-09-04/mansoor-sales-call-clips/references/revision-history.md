# Observed revision history and failure shields

This is the evidence behind the hard rules. Treat each correction as a reusable failure class.

## Editorial evolution

1. The early picture lock was about 64.57 seconds and contained avoidable pauses and rough joins.
2. A tighter pass removed the opening handle, filler and repeated words, pauses around or above 0.12 seconds, and a repeated closing word.
3. Over-tightening exposed the opposite risk: incomplete phone phrases and damaged word tails. The edit was rebuilt from the camera original to restore the client’s complete “first month” phrase and Mansoor’s complete “tomorrow.”
4. Later passes removed two residual micro-pauses and the final verified gap before Mansoor’s reply while protecting the adjacent word tails.
5. The approved final arc is 58.8 seconds. The lesson is not “always make it shorter”; it is “remove every avoidable pause without sacrificing a complete word, reaction, or necessary explanation.”

Failure shield: every cut requires transcript, waveform or listening, and cut-side frame review. A post-lock transcript difference reopens the cut.

## Client-speaker clarity

The viewer initially had no visible person on the other end of the call. The approved solution is to crop tightly into Mansoor holding the phone whenever the client speaks, use a yellow `CLIENT` pill and yellow captions, then return to the normal framing exactly when Mansoor resumes.

Failure shield: derive merged client intervals from the final caption timings and require exact one-to-one crop coverage. The validator rejects a late crop-in, late crop-out, missing client crop, extra crop, wrong vertical offset, or crop that leaks into Mansoor’s line.

## Headline placement and scale

The reviewer explicitly rejected a headline that felt too high. The approved relationship is immediately above Mansoor’s forehead or hair, not floating in unused space. A later correction rejected excessive white-box width and small type: “The white space is too wide… And you can make it bigger.”

Approved matching-footage values:

- `top: 235px`
- `left/right: 120px` for an 840 px box
- `font-size: 58px`
- `padding: 17px 22px 20px`
- two balanced lines, roughly 147 px total box height

Failure shield: the validator compares these values exactly. Manual QC additionally checks that the longest line fills the box and that the bottom edge sits about 0–20 px above the normal-crop hairline.

## Headline behavior

The user rejected the headline moving in and out and asked that it fade away after 10 seconds. Later batch review also rejected frames before the headline. The approved headline is fully visible on the first rendered frame, never changes position or scale, has no entrance, begins an opacity-only fade at 10.00 seconds, is absent by 10.35 seconds, and never returns.

Failure shield: only the opacity exit and optional seek-safe hard kill are allowed. Any fade-in, headline `x`, `y`, `top`, `scale`, rotation, repeated entrance, later reappearance, or altered fade time fails validation. If a close-up conflicts with the headline, move the camera image; do not move the headline.

## Identity protection

The original request required the client’s name to be cut out and covered by a level SFX. Merely laying a bleep over intact dialogue can leak the name.

Failure shield: the project privacy map lists every name interval. The validator requires a matching bleep interval and requires the dialogue volume automation to remain at zero across the entire mapped interval. Manual QC checks the name is absent from captions and inaudible on headphones and phone speakers.

## Captions

The corrected treatment uses white 68 px Mansoor captions at a fixed lower rail and yellow client captions with a `CLIENT` pill. Batch review explicitly rejected small multiword cards and an uncentered caption. Caption wording follows the verified final audio, not raw ASR, and is never summarized.

Failure shield: the validator locks the rail, 68 px typography, horizontal centering, no-wrap behavior, five-word maximum, client color, and speaker labels. Manual QC checks every audible word, spelling, financial terms, continuous coverage, and phone readability.

## 2026-09-03 batch-review failure cluster

Three consecutive clips exposed the same workflow weaknesses: blank or frozen frames before the headline, headline boxes too high or too small, captions that were too small or contained too many words, an uncentered caption, clipped first/final words, late crop-ins, crop changes inside a single client turn, Mansoor misclassified as the client, uncut pauses/glitchy joins, and endings before the payoff.

Failure shields:

- first-frame and `0.30 s` snapshots must both show moving footage and the same fully visible headline;
- `10.50 s` must show no surviving headline text, white container, shadow, or border; fade the complete styled box rather than a text-only child;
- every reviewer timestamp becomes a mandatory snapshot, plus a full-reel audit of the same defect class;
- crops are derived from final word-level speaker intervals, extend across pauses inside the same speaker turn, and reset only at the first following Mansoor phoneme;
- the final audio is re-transcribed after cutting and captions are segmented from that verified transcript at no more than five words per card;
- story QC must identify the explicit final resolution; a peak reaction without the decision/confirmation is incomplete;
- every picture lock is normalized to one-second keyframes before HyperFrames; sparse-keyframe or missing-frame warnings fail the render gate.


## 2026-09-04 Frame revision_final cluster (SC04 / SC05 / SC06)

On-disk dumps (not invented):

- `jobs/import:sales-call-04-felony:v1/workspace/output/frameio_reviews/revision_final.comments.md`
- `jobs/import:sales-call-05-twenty:v1/workspace/output/frameio_reviews/revision_final.comments.md`
- `jobs/import:sales-call-06-policy:v1/workspace/output/frameio_reviews/revision_final.comments.md`
- plus earlier `clip.comments.md` for each job

New reusable failure classes beyond the 2026-09-03 batch cluster:

1. **Flashing / lagging leftover frames** at joins (~0.5 s) — rejected on SC04/05/06 revision_final; clean-cut exemplar praised on SC05.
2. **Off-center opening** — “never start with footage that doesnt have him in center of frame” (SC05).
3. **Caption cropped by phone zoom** — “caption should never be cut off” / do not crop footage and caption together (SC06).
4. **Missing concluding resolution headline** — end with a 5–10 s (SC04) / ~7 s (SC05) one-sentence point-of-video card; SC06 requested an explicit redirect/buying-conversation line.
5. **Packaging doctrine (separate source):** archived Mansoor iMessage dump at `references/sales-call-feedback-2026-09-04/` (`…/context/mansoor/sales-call-feedback/2026-09-04-mansoor-imessage-upsell-feedback.md` + `.png`) — prefers objecting-handling / sales-presentation / policyholder-upsell value over thin proof-only packaging. See SKILL.md; not a Frame timestamp.

Verified repairs:

- SC04 v5 QC: flash removed; 6.0 s card “This is why you don’t give up on your clients.” (`qc/revision-v5/QC-REPORT.md`)
- SC05 v4 QC: opening centered; noted flash removed; 7.0 s resolution headline (`qc/v4-manual-qc.json`)
- SC06 spec lists a ~1.867–1.9 s closing card as an **approve-path outlier**; skill soft-default remains **~7 s** (SC05). Ivan may override later — do not block waiting on a duration decision.

Failure shields:

- contact-sheet every join ±0.5 s for flash/lag;
- first-frame center check for Mansoor;
- caption bounds check during every client crop midpoint;
- require `resolution_headline` / `resolution_card` in `sales-call-spec.json` with duration in the Frame band unless `approved_deviations` names a different hold;
- cite Frame dump paths when teaching a new rule — never fabricate comments.

See [frame-sourced-edit-rules.md](frame-sourced-edit-rules.md) for the full quoted extract.

## 2026-09-04 archive citation + soft-defaults

- Packaging doctrine source retargeted from task-text-only to the on-disk iMessage archive (`references/sales-call-feedback-2026-09-04/` → content-ops `context/mansoor/sales-call-feedback/` md+png). Citations quote/summarize that dump only.
- Soft-default concluding/closing headline hold: **~7 s** (SC05). SC06 ~1.867–1.9 s remains an approve-path outlier.
- Soft-default packaging priority when Mansoor/Ivan names an upsell/objection/presentation beat; keep **one** skill (no split until Ivan asks).

## Delivery and Frame.io

An earlier Frame share displayed “Please try again later” even though upload or transcode state appeared healthy. Version-stack state by itself did not prove public playback.

Failure shield: keep the stable review context, but verify the actual intended asset is `transcoded`, request the public deep link, follow redirects, require HTTP 200, and confirm the returned page identifies the new filename. When a stack fails publicly, retain it for internal history and attach the latest standalone asset to the same public share as a fallback.

## Final approved reference

- Format: 1080×1920 H.264/AAC
- Runtime: 58.8 seconds
- File size: 93,938,524 bytes
- Headline: compact 840 px box, 58 px type, fixed position, gone after the 10-second fade
- Client crop: `scale: 2.35`, origin `78% 58%`, exact speaker-boundary intervals
- Privacy: original name audio muted and replaced by a matched level bleep
- Delivery: public Frame viewer verified after transcode
