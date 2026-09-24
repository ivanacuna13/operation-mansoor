# How Ivan clips (visual equivalent of Premiere)

Source: `Downloads/how to clip screen recording.mp4` (2026-08-12). Full transcript: `Desktop/AIDA/how-to-clip-watch/how-to-clip.elevenlabs.txt`. Stills in that same folder.

If you are an agent: he is in Premiere Pro. Do the **visual equivalent**. Do not invent a looser process. This recording overrides older clip_qc placement/stacking rules where they conflict.

Related: `clip_selection.md`, `process_clipedit.md`, `clip_qc.md`, `instagram_safe_zones.md`.

---

## 1. Selection is engineering a message

Not “a cool moment.” Not a timestamp dump.

1. Hear a **hook that promises** (example: “the biggest mistake people do…”). That promise is the reason the clip exists.
2. Pick the **end as delivery** of that promise (downward intonation, value landed, identity locked). Incomplete examples and extra “so any action…” loops are not an ending.
3. Hold the **whole video’s value proposition** in your head while you cut (here: how to structure a routine so emotion → action → identity). The clip must deliver a point from that broader context, not a free-floating quote.
4. Selection ≠ approval to ship. After the range exists, you still condense.

If you cannot say the value proposition in one breath, kill it.

## 2. Condense for value per second

Platforms will take 90 seconds. That is not the bar. Cut fluff until it is dense.

Cut automatically:
- um / uh / false starts / “so” as a filler
- additive setup (“because the principle here is the following”)
- repeats of the same sentence two ways
- incomplete examples
- long-form reinforcement of a sentence already landed (hunger / sleep / sales-call paragraph when the hit is “emotion is the foundation of all action”)
- “now” + the pause after it
- “guess what happens”

After a cut, the remaining transcript must still **read as good writing** out of context. If it doesn’t, the cut is wrong.

Worked example from the recording: ~90s → ~1:10 → **44 seconds**.

## 3. The cut is the waveform (mechanical truth)

Transcript and silence detection are drafts. They stutter.

Premiere move → equivalent:
- Razor on the timeline, then **ripple delete**
- Zoom the **audio waveform** until you see the gap
- Align the cut to the **start of the next word**, not the silence detector’s guess
- Premiere’s “dot dot dot” (~0.1s) is still a pause — close it
- Play back: if the wave looks continuous, the viewer will not register a cut
- A small **visual jump is allowed** if audio flows. Never slice a word.

If your tools cannot show a waveform, you cannot make these cuts. Do not ship transcript-only edits.

## 4. Picture

This style (Mansoor talking, high-res enough): **full-screen 9:16**, face fill, scale ~180–184%, not square-stack blur.

## 5. Headline then captions (do not stack)

First ~4 seconds: **text hook / headline** only. Captions off. All eyes on the headline.

Then captions. Never headline + caption fighting for the same moment.

Headline rules:
- Comes from the value proposition + a curiosity gap
- Complements the verbal hook — **do not repeat** what he is about to say
- Use real context you have (here: $3M year after the routine) when it is true
- Center-aligned, dead center, around the **chin**
- At most **two lines**, not top-heavy or bottom-heavy
- Stays out of Instagram red zones
- Filename of the export **is the headline**

## 6. Caption style (this look)

From the recording, exact:
- Font: **Manrope Regular**
- Max length: **23 characters**
- Min duration: **2 seconds**
- **Single line only. Double lines forbidden.**
- Tracking: **-27**
- Size: **23**
- Position: **70 units down** (on the chin, just below the mouth — not on the face, not in a generic mid-frame box)
- Fill: white
- Slight black shadow (see stills / Premiere properties)
- Punctuation clean; no filler crumbs on screen

If a headline is up, skip the caption for that beat.

## 7. Music (optional)

Teaching/talking can ship with **no music**.

If music:
- Instrumental from the trending library
- Never overpower speech
- His vocals hover about **0 to -3 dB** (around **-1** while talking)
- Music about **-18 to -20 dB**
- Flat beds don’t need extra automation; save that for another pass

## 8. Export

- Sequence: **1080×1920**, native frame rate
- H.264, hardware encoding
- Target bitrate **10–12 Mbps**
- Render at maximum depth + maximum render quality
- **Burn captions** into the file
- In/out of the selected range only
- Name = headline

## 9. What “done” looks like

A stranger can watch 44 seconds, get the promise, and never feel a cut. Headline hooks, captions sit on the chin, audio is one continuous take. Waveform evidence exists for every ripple. Transcript-only QC is not done.
