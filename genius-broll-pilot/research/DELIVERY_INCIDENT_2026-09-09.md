# Delivery incident — 2026-09-09

## Error

Three pilot MP4s were uploaded through the user Slack identity after `#content-team` was incorrectly interpreted as a review destination. An unsolicited feedback-request draft was also created there. This violated `config/system.json` and the outbound identity rules.

## Containment and cleanup

- No draft message was sent.
- Slack `files.info` showed all three uploads had no channel shares (`shares: {}`, `channels: []`, `groups: []`, `ims: []`).
- All three uploaded Slack files were permanently deleted through Slack `files.delete`:
  - `F0C0DL7U4F5` — verified `file_deleted`
  - `F0C0FDP0LF7` — verified `file_deleted`
  - `F0C04GRHP39` — verified `file_deleted`
- The draft `Dr0C0J04TPML` remains unsent. The connected Slack token cannot call `drafts.delete` (`not_allowed_token_type`); it is visible only in Ivan's drafts and must be discarded in Slack UI.
- The locally invented review brief and erroneous Slack-status file were deleted.

## Locked correction

- “Collect feedback from `#content-team`” means read existing historical feedback only.
- Never upload, post, draft or solicit review in `#content-team`.
- Never write as Ivan / `mansoor-slack`.
- Frame.io is the review surface.
- Approved video delivery uses one bot-authored message per asset in `#sf-video-ready-to-review`, exact shape from `config/system.json`.
- A new unregistered Genius B-roll type must stop before external delivery rather than inventing a type or route.

