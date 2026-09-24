# Approved visual specification

This specification comes from the approved IUL good-news V5. Use it literally for matching seated, portrait phone-call footage. If source geometry differs, follow the calibration section; do not guess.

## Canvas and base framing

- Canvas: `1080×1920`, square pixels, 9:16.
- Delivery frame rate: preserve the source cadence; the approved reference is `30000/1001`.
- For matching 3840×2160 landscape footage, the approved center portrait extraction is `crop=1215:2160:(iw-ow)/2:0`, then `scale=1080:1920`.
- At the normal crop, keep Mansoor’s entire head, shoulders, phone, and enough torso for stable framing. Do not zoom the base shot merely to create energy.

## Headline: exact approved profile

```css
#premise {
  position: absolute;
  top: 235px;
  left: 120px;
  right: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 17px 22px 20px;
  border: 0;
  border-radius: 12px;
  color: #111;
  background: #fff;
  box-shadow: 0 10px 34px rgba(0,0,0,.24);
  font-size: 58px;
  line-height: .96;
  font-weight: 900;
  letter-spacing: -.05em;
  text-align: center;
  text-transform: none;
}
```

Hard requirements:

- The box is 840 px wide because side margins are 120 px. Do not return to near-edge 60 px margins.
- Use 58 px type for the approved two-line treatment. Do not shrink to the provisional 48 px treatment.
- Use no more than two lines. Insert a deliberate line break with balanced line lengths.
- The longest line should visually fill roughly 82–94% of the inner width. If it leaves broad empty white space, shorten the box or rewrite the headline; do not accept a loose oversized container.
- Keep compact padding. The reference box is about 147 px tall for two lines.
- At normal crop, the bottom of the box sits immediately above Mansoor’s hair or forehead, with approximately 0–20 px of visual separation. It must not float in unused space.
- The box may approach hair but may not cover an eye. During crop-ins, preserve at least one clearly visible eye or another strong facial identity anchor.

### Headline motion

The headline is static and fully visible on the first rendered frame. It has no entrance animation; opacity is used only for the single exit. Animate the complete styled box, never only the text inside it.

```js
tl.to("#premise", { opacity: 0, duration: 0.35, ease: "power1.out" }, 10.00);
tl.set("#premise", { opacity: 0 }, 10.35);
```

- Do not animate `x`, `y`, `top`, `scale`, rotation, or repeated entrances and exits.
- It is fully legible at `t=0.00`, remains fixed, starts fading at 10.00 s, is fully absent by 10.35 s, and never returns.
- The element can remain timed for the full composition, but its opacity must stay zero after the fade.
- At `10.50 s`, neither text, white background, shadow, border, nor padding may remain visible.


## Opening framing

- First rendered frame: moving footage + fully visible opening headline.
- Mansoor’s head/torso must be centered enough that the open does not feel like the camera is pointed away from him (Frame SC05 revision_final).
- Reject still holds, blank frames, and off-center opens unless the project brief documents an explicit approved deviation.

## Concluding resolution headline

After the final kept spoken content, show a second headline/card that states the video’s point or resolution. This is separate from the opening premise headline that fades by 10.35 s.

Hard requirements from Frame revision_final dumps (SC04/05/06):

- One short sentence is enough.
- **Soft-default hold: ~7 seconds** (SC05 Frame exemplar). Frame SC04 also allows a **5–10 second** band. SC06’s approved ~1.867–1.9 s closing card is an approve-path outlier — use only via `approved_deviations`; do not wait on Ivan for a duration decision.
- Examples actually requested in Frame (do not reuse blindly on unrelated clips):
  - “this is why you don't give up on your clients” (SC04)
  - “Another family protected ✅” (SC05)
  - “client successfully redirected into buying conversation” (SC06)
- Prefer the same compact white-box geometry family as the opening headline unless the project already approved a full-bleed card treatment (SC04 used a contextual card over a still; record the chosen treatment in the project spec).
- No position/scale animation on the concluding card; opacity fades only if needed for a clean out.
- Save text, start, end, and duration in `sales-call-spec.json` under `resolution_headline` or `resolution_card`.

## Caption profile

```css
.caption {
  position: absolute;
  top: 1320px;
  left: 72px;
  right: 72px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  text-align: center;
}
.caption-text {
  max-width: 100%;
  color: #fffdf7;
  font-size: 68px;
  line-height: 1;
  font-weight: 800;
  letter-spacing: -.055em;
  white-space: nowrap;
  text-shadow: 0 4px 3px rgba(0,0,0,.94), 0 0 20px rgba(0,0,0,.72);
}
.caption.client .caption-text { color: #ffe171; }
.speaker {
  padding: 8px 15px 9px;
  border-radius: 999px;
  color: #17130a;
  background: #ffe171;
  font-size: 23px;
  line-height: 1;
  font-weight: 900;
  letter-spacing: .055em;
  text-transform: uppercase;
}
```

- Client captions say `CLIENT`; do not expose a personal name.
- Every caption card is one centered line with at most five spoken words. Target four or five words; use fewer only for a short response or natural sentence ending. Never shrink the approved 68 px type to fit more words.
- A restrained caption entrance may use opacity plus an 18 px vertical settle and `0.985→1` scale over about 0.13 s. It must be seek-safe and must not delay legibility.
- Do not move the caption rail between speaker types.
- Never crop captions off-frame during a phone close-up. If the crop and caption collide, reduce crop scale / adjust origin or raise/lower within approved calibration — do not slice the caption (Frame SC06 revision_final).

## Client phone close-up

For the approved matching footage:

```js
tl.set("#camera-outer", { scale: 2.35, transformOrigin: "78% 58%" }, start);
tl.set("#camera-inner", { x: 0, y }, start);
tl.set("#camera-outer", { scale: 1, transformOrigin: "50% 50%" }, end);
tl.set("#camera-inner", { x: 0, y: 0 }, end);
```

- `scale: 2.35` and origin `78% 58%` are the approved same-framing values.
- Use a direct state change at speaker boundaries. Do not drift, pulse, or alternate crops inside an utterance.
- The close-up must make the phone unmistakable and retain a facial identity anchor: at least one eye, or a clear mouth and beard area with the phone.
- Client close-up intervals must exactly cover the merged client-caption intervals. No client interval may lack a crop; no Mansoor interval may inherit one.
- When a client response occurs while the headline is visible, use the project-calibrated camera-inner vertical offset. The IUL reference uses `y: 150` for the early `6.16–6.72` response so the fixed headline does not cover the eye. Keep the headline stationary.

## Calibration for materially different source framing

Only these values may be calibrated without a new user direction:

- headline `top`, to maintain the immediate-above-forehead relationship;
- phone close-up `transformOrigin` and early-window inner `y`, to retain the phone and facial anchor.

Do not change side margins, headline font size, box padding, fade timing, caption rail, client colors, crop timing, output dimensions, duration cap, or size cap merely because the source differs.

Before accepting calibrated values, render and inspect:

1. `0.00 s` and `0.30 s`: moving footage is present and the headline is fully visible at identical coordinates.
2. Midpoint of every client interval before `10.35 s`: headline plus close-up; eye or identity anchor clear.
3. `9.90 s`: headline fully visible and stationary.
4. `10.20 s`: headline mid-fade only; no movement.
5. `10.50 s`: headline absent.
6. Midpoint of every later client interval: phone close-up and client label visible.
7. First Mansoor frame after each client interval: normal crop restored.
8. First frame of the concluding resolution headline/card: text fully legible; duration matches the project spec (soft-default ~7 s; SC04 5–10 s band; non-default only if approved).
9. Final frame: clean end on the resolution card (no flash cut to black mid-card unless specified).

## Automatic rejection conditions

- Headline is high in empty space rather than immediately above the forehead.
- White box is wider than the text needs, type is visibly small, or padding creates dead space.
- Headline moves, scales, re-enters, flickers, or survives beyond the fade window.
- A blank frame, still-image hold, or frozen opening appears before or beneath the headline.
- Opening footage does not center Mansoor.
- Flashing, lagging, or leftover half-second frames appear at any join.
- Missing concluding resolution headline/card, or a hold far from the ~7 s soft-default (or outside the SC04 5–10 s band) without an approved deviation.
- Phone close-up crops captions off the frame.
- Any crop covers both eyes while leaving unnecessary background.
- Crop begins late, ends late, oscillates during client speech, or remains while Mansoor talks.
- Phone is not obvious during client speech.
- Caption wraps, collides with UI-safe edges, covers the important face or phone area, or lacks the `CLIENT` distinction.
- A caption contains more than five spoken words, is not horizontally centered, paraphrases the audio, or omits an audible filler/word.
