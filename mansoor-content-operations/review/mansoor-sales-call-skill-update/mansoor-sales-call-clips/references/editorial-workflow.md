# Editorial workflow

## Source truth and preparation

1. Confirm the exact camera original by path, duration, frame rate, dimensions, and audio streams. Do not select by filename similarity alone.
2. Preserve the original. Work from a project copy or proxy and retain a path back to the original.
3. Generate word timestamps and manually identify `mansoor`, `client`, and `unknown`. Phone audio is often quieter or less distinct; listen to ambiguous phrases rather than deleting them as silence.
4. Search the complete call for names, not just the selected arc. Mark every selected name interval to phoneme boundaries.
5. Create an edit-map entry for every kept section:

```json
{
  "id": "client-reaction",
  "speaker": "client",
  "source_start": 26.32,
  "source_end": 27.68,
  "out_start": 11.04,
  "out_end": 12.16
}
```

## Story selection

The reel should feel like the viewer witnessed a real call, not a stitched testimonial.

Keep this order unless the recording itself requires a smaller, truthful reordering:

1. Mansoor establishes the client’s prior problem or why the news matters.
2. Mansoor states the turnaround or approval.
3. Preserve the client’s first genuine reaction in full.
4. Keep the minimum follow-up that proves the outcome is real and understandable.
5. End on a clean conversational resolution after the peak moment: confirmation, client decision, agreed number, next step, or Mansoor's final commitment. If the selected ending sounds like the call continues or withholds the result, keep searching forward.

Start on speech or immediately before its onset. The first rendered frame must contain moving source footage and the fully visible headline. Do not use silent phone setup, dialing, waiting, camera settling, repeated greetings, off-premise conversation, a blank lead-in, or a still/freeze-frame intro. The headline supplies premise context; Mansoor’s first line supplies authenticity.

## Dialogue cutting

- Remove repeated words, false starts, filler, correction loops, and dead air.
- At edit seams, target no avoidable silent gap longer than about 0.12 seconds. This is a review trigger, not permission to cut through a word or a meaningful reaction breath.
- Preserve every first consonant and final vowel or consonant release. A complete phrase outranks a shorter runtime.
- Inspect the waveform and listen around both sides of every cut. Retain a tiny nonspeech handle; use a 3–8 ms fade only to eliminate a click.
- Never use a long crossfade across speech. It can double room tone or smear consonants.
- Re-transcribe the picture lock. A changed, missing, or substituted word reopens that join.
- Specifically inspect the last word before every cut. The IUL revision history exposed incomplete reaction phrases, a missing “first month,” and a clipped “tomorrow”; these are failure classes, not isolated words.

## Client speaker treatment

Build merged client intervals from the final picture lock. Adjacent client caption phrases separated by no more than 0.16 seconds are one continuous interval. For each interval:

- start the close-up at the first client phoneme;
- hold one stable close-up for the entire interval;
- end it at the first following Mansoor phoneme;
- show the yellow `CLIENT` pill for every client caption phrase;
- do not leave the client crop active while Mansoor answers.

The crop is a speaker-identification device. It must visibly feature Mansoor holding the phone and a facial identity anchor. It is not a random emphasis zoom.

## Captions

- Write from the verified final dialogue. ASR is a timing aid only. Do not summarize, sanitize, or omit any word or filler that remains audible.
- Use sentence case and natural punctuation. Do not sanitize the client’s real reaction.
- Keep each displayed phrase on one line in the approved caption safe area at 68 px. Use no more than five spoken words per card; target four or five and permit a shorter card only for a natural sentence ending or brief response.
- Cover consecutive speech continuously; do not leave an unexplained caption hole.
- Mansoor: white caption. Client: yellow caption plus yellow `CLIENT` pill.
- Check every financial term, number, policy term, and contraction character by character.
- Do not display the client’s name. Use an em dash or restructure the phrase without changing its meaning.

## Privacy bleep

For every selected client-name occurrence:

1. Mark the true phoneme onset and release by listening and waveform inspection.
2. Automate dialogue to zero across the full interval, with only click-safe edge ramps outside the name.
3. Place the same bleep SFX over the same interval at one consistent gain.
4. Listen soloed, in mix, on headphones, and at phone volume. No identifiable syllable may remain before, under, or after the bleep.
5. Confirm the bleep is level with the program: clearly masks the name without a startling loudness jump.
6. Inspect the caption at the same frame; the name must not appear in text.

## Audio finish

- Dialogue is the priority. Keep the phone response intelligible without making it unnaturally louder than Mansoor.
- Remove clicks and obvious boundary changes; do not flatten the human reaction.
- Do not add music unless the user asks for it or an established project direction requires it. If used, Mansoor’s standing direction rejects hip-hop; use an audible non-hip-hop cinematic or motivational bed and keep speech effortless to understand.

## HyperFrames media preparation

- Re-encode the final picture lock to constant 30 fps H.264 with `-g 30 -keyint_min 30 -sc_threshold 0` before authoring or rendering.
- Probe keyframe timestamps and require the maximum interval to be no more than 1.10 seconds.
- Any HyperFrames sparse-keyframe, seek-failure, missing-frame, or frame-freeze warning reopens media preparation and requires a new normalized picture lock.
