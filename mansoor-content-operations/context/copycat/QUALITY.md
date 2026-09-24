# Lifestyle Copycat QC gate

Parked 2026-08-17. Ivan: quality drastically down. Super shit audio, bad text hooks, frozen frames.

Do not Slack a cut until this file is PASS. Run it on the export. If any check fails, do not upload, do not Slack, recut.

Open this every cut with CUTTER_PATH.

---

## 1. Frozen frames (hard fail)

A motion clip that holds still is a glitch. Ivan ❌'d it.

Before Slack:

```
ffmpeg -i "<export>" -vf "freezedetect=n=0.003:d=0.4" -map 0:v -f null -
```

Any `freeze_start` on a motion clip = FAIL. Recut. Do not pad with last frame, tpad, freeze, or loop_clip.

Photo stills only when the original is a still or Ivan asked for a still (homeless still IMG_5004). A still held as video still cannot sit next to a freeze-padded clip.

Never fill duration by freezing the last frame. If the hold is longer than the file, cut to a different unused file.

Known already-shipped freezes (do not treat as the bar):
- Man, you worrying about the wrong thing.mp4 — 3.2s freeze at 4.23
- If you don't listen in school... — freeze at 8s
- It's rare, but some people genuinely want to see you win — 3s freeze at 0
- Getting free with bro — 1.2s freeze
- I'm gonna make it momma v2 — 1s freeze
- i had nothing to my name 3 years ago — 2.2s freeze

---

## 2. Audio (hard fail)

Listen to the mux. Do not trust ffprobe.

FAIL if:
- muffled, whisper, thin, crushed
- wrong track
- missing, clipped, or shorter than the picture
- Instagram-ripped HE-AAC / sub-80kbps source shipped as the mix (tofu/bryson rips are often 47kbps — that sounds like shit)
- profane lyrics playing (swap to instrumental, MUSIC.md)

PASS: full energy, same drop as the original, clean. Duration = original audio exactly.

If the ripped IG file is thin, do not ship it. Find a clean version of the same song (or an instrumental of the same energy). Mux that.

---

## 3. Text hook (hard fail)

The on-screen line is the product. Ivan ❌'d sloppy hooks.

PASS:
- steals the original's card count and joke shape
- viewer-ICP (18–28 dropout, send to the boy or mom)
- short enough to read in the hold
- pictures prove the line

FAIL:
- caption dump / essay on screen
- about the offer, Mansoor, or a brand
- a different joke than the original framework
- a shortcode as the line

The killed Plan A line (`find a good girl get married have kids / be the uncle who made it anyway`) is the example of a bad hook. Do not write another one like it.

---

## Gate (every export, in this order)

1. Watch the cut. Face first ~3s, Mansoor not dad, no wife face, no same-shot glitch.
2. Listen to the audio all the way through.
3. Read the on-screen line out loud. Would the boy send it.
4. Run freezedetect. Zero motion freezes.
5. Only then upload and Slack.

No gate, no Slack.

---

## How a cut runs (Ivan 2026-08-17)

Cutter owns this motion. Eddie stays out unless something is actually broken.

1. Cutter watches Ready to Edit. When one remake is ready, Cutter starts one worker for that one video.
2. One remake, one worker. Never two. Never a pile.
3. The worker ticket is a full stranger brief: CUTTER_PATH, this file, STELLAR, MISTAKES, REVIEW_LOG, the one ready-to-edit card, unused-clip check.
4. Never tell the worker to skip the rules or just ship.
5. The worker only cuts. It does not Slack. It does not QC itself.
6. Cutter runs this gate on the export: watch, listen, read the hook, freezedetect.
7. PASS → Cutter Slacks. FAIL → do not Slack, recut or stop.
8. The worker does not start another worker.

Do not notify Eddie about ordinary cuts. Ivan reviews in Slack.
