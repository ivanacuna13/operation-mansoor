# Revision v5 QC Report

- Deliverable: `final/Mansoor-Sales-Call-04-Felony-Eligibility-v5.mp4`
- SHA-256: `813723df33a44a1a2f47fd4389245067ed98146d25131dae4fbeb32c692293b6`
- Size: 126,567,478 bytes
- Runtime: 52.800 seconds
- Format: H.264 High, 1080x1920, 30 fps; AAC-LC stereo, 48 kHz
- Full FFmpeg decode: pass
- Sales-call deterministic validator: pass (35/35)
- HyperFrames full check: pass (214 samples, including transitions and revision boundaries)
- Integrated loudness: -16.9 LUFS
- True peak: -1.3 dBFS
- Loudness range: 8.7 LU

## Revision-note verification

1. The residual 0.32-second visual interval at the 42.16-second edit was removed. A 30 fps boundary contact sheet and scene-change scan show one clean source cut at 42.1667 seconds, followed by normal picture levels (luma means 101 and 95); no black, blank, or flashing frame remains.
2. Spoken content ends at 46.8 seconds, followed by a six-second contextual card: “This is why you don’t give up on your clients.”

## Manual visual and transcript audit

- Inspected the full-video contact sheet plus critical frames at the opening headline, headline exit, all phone-speaker crop boundaries, the repaired join, dialogue end, and resolution-card hold.
- No unintended black frames, caption gaps, crop regressions, stale headline returns, or card truncation observed.
- Fresh local `faster-whisper-small` transcription completed from the rendered MP4 (164 words). Dialogue ends with “So five years on the conviction. Okay, okay.” and contains no extra speech under the six-second card.
- Existing name privacy bleep remains in place and passed the validator’s interval/mute checks.

## Evidence

- `automated-qc.txt`
- `ffprobe.json`
- `boundary-42s-contact.png`
- `critical-contact.png`
- `full-contact.png`
- `transcription/transcript.json`
