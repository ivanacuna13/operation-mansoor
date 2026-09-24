# Ready to Post

CODE tool that files green-checked videos into Google Drive **Ready to Post** day buckets and appends a ledger row. **No Slack. No Post Bridge.**

## Layout

```
Ready to Post / {Month YYYY} / {DD} / {type_folder} / {Clean Title}.mp4
```

Example: `Mansoor Content/Ready to Post/September 2026/06/BOF Scripted Talking Heads/My Headline.mp4`

Config: `config/system.json` → `drive.ready_to_post`  
Day folder ID cache: `/workspace/drive-backfill/day_ids.json`  
rclone remote: `gdrive:` (paths addressed with `--drive-root-folder-id`)

## Caps (America/Chicago)

| Funnel | Max / day | Type folders |
|--------|-----------|--------------|
| TOF    | 6         | TOF Copy Cats, TOF Static Reels |
| MOF    | 2         | MOF Genius Clips |
| BOF    | 2         | BOF Scripted Talking Heads, BOF Sales Call Clips, BOF Sales Call Skits |
| Day total | ≤ 10   | all type folders above |

Walk forward from today (or `--date`) until the first day where **funnel count < max** and **day total < 10**. Missing type folders are created with `rclone mkdir`.

## Format → type folder

| Format aliases | Dest folder |
|----------------|-------------|
| Lifestyle Copycat, TOF Copycat, Copycat | TOF Copy Cats |
| Static Reel, TOF Static Reel | TOF Static Reels |
| Genius Clip | MOF Genius Clips |
| Scripted Talking Head | BOF Scripted Talking Heads |
| Sales Call Clip, Mansoor Sales Call Clip | BOF Sales Call Clips |
| Sales Call Skit, Sales Call Roleplay | BOF Sales Call Skits |

Already-prefixed names are accepted as-is.

## CLI

```bash
# Pick first day with room
python3 ready_to_post.py pick-day --format "Genius Clip"
python3 ready_to_post.py pick-day --format "Scripted Talking Head" --date 2026-09-05

# File from packet JSON
python3 ready_to_post.py file --packet-file /path/packet.json
python3 ready_to_post.py file --packet-file /path/packet.json --dry-run

# File from explicit source
python3 ready_to_post.py file \
  --source-url-or-path /path/video.mp4 \
  --format "Genius Clip" \
  --title "My Headline" \
  --content-page-id optional-notion-id
```

Packet fields (flexible): `format` / `content_format`, `frame_link` / `file_url` / `drive_file_id` / `source_path`, `headline` / `title`, `content_page_id` / `notion_id`, `channels`.

### Copy sources

1. Drive file id or Drive URL → `rclone backend copyid` (server-side when possible)
2. Local `source_path` → `rclone copyto`
3. Frame.io / http(s) URL → download to `/workspace/ready-to-post-tmp`, then `rclone copyto` (best effort; failure returns `ok=false`)

Originals are **copied**, never deleted.

## Output

Stdout is a single JSON object:

```json
{
  "ok": true,
  "funnel": "MOF",
  "type_folder": "MOF Genius Clips",
  "month": "September 2026",
  "day": "05",
  "dest_folder_id": "...",
  "dest_url": "https://drive.google.com/...",
  "drive_path": "Mansoor Content/Ready to Post/September 2026/05/MOF Genius Clips/...",
  "error": null
}
```

Ledger (append JSONL): `/home/box/mansoor-content-operations/state/ready-to-post-ledger.jsonl`

## Do not

- Post to Slack / `#sf-ready-to-post`
- Call Auto Post Bridge
- Invent type folder names
- Overfill funnel or day caps
