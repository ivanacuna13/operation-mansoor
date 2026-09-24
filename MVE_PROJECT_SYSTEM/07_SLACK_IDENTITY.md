# Slack identity freeze — MVE reaction / delivery channels

Date: 2026-09-08 (PT)  
Source: `/home/box/mansoor-content-operations/config/system.json` + live `mve.py` `JOB_REGISTRY`

## Live video delivery (SoT)

| Role | Name | ID |
|---|---|---|
| Video ready-to-review (live MVE delivery + primary reaction channel) | `#sf-video-ready-to-review` | `C0BVAAVASV7` |
| Historical human content-team (assets may still map here) | `#content-team` | `C0BQKM27F5F` |
| Legacy ai-content-team (deprecated for SF deliverables) | `#ai-content-team` | `C0BV0Q7JZ6H` |
| Lifestyle Copycat delivery + Eddie emoji review loop | `#lifestyle-copycats` | `C0BQTR6RP97` |

`CONTENT_TEAM` in `mve.py` resolves from `slack.video_delivery_channel_id` → `C0BVAAVASV7`.

## MVE `cmd_reaction` channel allowlist

Accepted (memo / ✅ / ❌):

1. `video_delivery_channel_id` → `C0BVAAVASV7`
2. `human_content_team_channel_id` → `C0BQKM27F5F` (if present)
3. `legacy_ai_content_team_channel_id` → `C0BV0Q7JZ6H` (if present)

Rejected / ignored by MVE reactions:

- `lifestyle_copycat_channel_id` → `C0BQTR6RP97` — **Eddie owns** the Lifestyle emoji loop; do not force lifestyle through MVE memo/reaction map.

Dry check (no Codex):

```bash
python3 .../mve.py reaction-channel-check --channel-id C0BVAAVASV7
python3 .../mve.py reaction-channel-check --channel-id C0BQKM27F5F
python3 .../mve.py reaction-channel-check --channel-id C0BV0Q7JZ6H
python3 .../mve.py reaction-channel-check --channel-id C0BQTR6RP97
```

## TYPE labels (delivery)

From `system.json` `slack.video_delivery_format` (and aligned docs):

| job_type | Slack TYPE |
|---|---|
| `sales_call_clip` | `BOF Sales Call Clips` |
| `scripted_talking_head` | `BOF Scripted Talking Heads` |
| `genius_clip` | `MOF Genius Clips` (registry `slack_type` may still say `Genius Clip`) |
| `lifestyle_copycat` | `TOF Copy Cats` / `Lifestyle Copycat` |

Outbound Slackbot: `copycat-cutter`. Never post as Ivan. Authorized reviewers: allowlist in system.json (includes Ivan `U0BQJP0DEGH`).

## `#ai-content-team` note

Deprecated for SF deliverables. Scripts → `#sf-scripts-ready-to-review`; videos → `#sf-video-ready-to-review`. Kept on reaction allowlist only so historical mapped messages still revise.
