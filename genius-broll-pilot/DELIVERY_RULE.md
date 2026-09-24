# Delivery rule — source of truth

Source: `mansoor-content-operations/config/system.json`, reinforced by `CONTENT_PM.md` and `MASTER_VIDEO_EDITOR.md`.

- `#content-team` (`C0BQKM27F5F`) is human-ops context. For this work it is read-only research: read existing feedback only. Never upload a video, ask for feedback, draft a message or post as Ivan there.
- Review assets go to Frame.io first. Playback and the correct asset/version must be verified.
- Video review delivery goes to `#sf-video-ready-to-review` (`C0BVAAVASV7`).
- Slack write identity is the `copycat-cutter` bot (`U0BQGU4FVU5`), never Ivan / `mansoor-slack`.
- One top-level message per item; no invented questionnaire and no status chatter.
- For the registered Genius route, the exact current shape is:

  ```text
  TYPE: MOF Genius Clips
  PLATFORM: Instagram
  FILE: {verified_frameio_url}
  ```

- A new Genius B-roll type must not be silently invented in production configuration. Until the type is explicitly registered, use the closest authorized pilot route only if Ivan confirms it; otherwise stop before delivery.
- Pilot 03 remains private and cannot enter the public delivery path until outside-audio rights and attribution are resolved.
