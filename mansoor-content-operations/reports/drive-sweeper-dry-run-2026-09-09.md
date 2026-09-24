# Mansoor Drive Sweeper — Read-Only Dry Run

**Run date:** 2026-09-09  
**Scope:** Google Drive folder `upload here` only  
**Mode:** Read-only simulation  
**Drive mutations:** None  
**Slack actions:** None  

## Executive summary

The upload inbox currently contains **13 files**.

- **4 recent video candidates** were uploaded/modified on September 1–3, 2026.
- **8 older temporary video files** appear to be processing leftovers from August 21.
- **1 older audio file** was uploaded on August 16.
- No files were renamed, moved, copied, deleted, or trashed.

The sweeper rules require identifying footage from the actual media and transcript—not from filenames. The two files with usable Drive transcripts can be classified. The two DJI files are visibly Mansoor talking-head footage, but their exact scripts/titles are not confirmed because Drive did not expose transcripts for them. In a real run, those two would remain in the inbox until identified.

## Before state — actual Drive state

All 13 files were directly inside the [Mansoor upload inbox](https://drive.google.com/drive/folders/1YKEGX9LH2Vt1akvVmCII2lUVKBUtfzGa).

### Recent video candidates

| Current filename | Drive file | Size | Drive created | Media evidence | Dry-run classification |
|---|---|---:|---|---|---|
| `DJI_20260903130014_0007_D.MP4` | [Open](https://drive.google.com/file/d/1TRh_hPiGAQUKFJbsHsLV5S1XD9Ct1hKk/view) | 4.29 GB | 2026-09-03 | Mansoor talking head, portrait framing; approx. 13:25; no transcript exposed | Scripted talking head, title unresolved |
| `DJI_20260903124353_0006_D.MP4` | [Open](https://drive.google.com/file/d/1AHxfbr_9RWwKB-F5xcu_nSK4I_BZKi8W/view) | 4.60 GB | 2026-09-03 | Mansoor talking head, close-up framing; approx. 15:23; no transcript exposed | Scripted talking head, title unresolved |
| `haz sales call.MP4` | [Open](https://drive.google.com/file/d/1BYhLufUliiwfCuChFJRODvDHvdol-CvG/view) | 3.12 GB | 2026-09-01 | 7:32 transcript: Chaz, policy approval, premiums, and front-loading | Sales call |
| `1` | [Open](https://drive.google.com/file/d/1NnDZ4CyaFxRCX8yqqwTvD5vb9caSuhYY/view) | 2.11 GB | 2026-09-01 | 7:02 transcript: “biggest lie” in the life-insurance industry; argues agents need both sales and team leverage | Scripted talking head |

### Older files left in the inbox

These were not treated as part of the recent September candidate batch. Their names are processing-style names, but the sweeper is not allowed to classify files from filenames alone.

| Current filename | Drive file | Size | Drive created | Dry-run treatment |
|---|---|---:|---|---|
| `tmp-clip-export-0058b.mp4` | [Open](https://drive.google.com/file/d/1FERrz_dFipOFtvUEfoOA0k7bj18ZI2Jp/view) | 4.65 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-clip-export-0054.mp4` | [Open](https://drive.google.com/file/d/1LxegNEqSK9hiacoj0lHhjp_45Hppk7Cu/view) | 17.19 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-clip-export-0058.mp4` | [Open](https://drive.google.com/file/d/153yv1bVZVDmrnAiHmE9qJ5ZJGnryAZHg/view) | 4.65 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-src-0058c.mp4` | [Open](https://drive.google.com/file/d/1yX8qyo4JFvOuwfRWxbUtZmMNmlxKuI5b/view) | 4.65 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-src-0058b.mp4` | [Open](https://drive.google.com/file/d/1o31Ymc5EckOMNTkv6emv0TMVDmYT2T4X/view) | 4.65 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-audio-extract-0054.mp4` | [Open](https://drive.google.com/file/d/1tUXHJODKAiG5mStQ5leHcPd5Ymwvv0LT/view) | 17.19 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-audio-extract-0054.mp4` | [Open](https://drive.google.com/file/d/1Xr8qc1uQoGA3K0Ptra-JPQF9InDrA6Oh/view) | 17.19 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `tmp-audio-extract-0058.mp4` | [Open](https://drive.google.com/file/d/1lBYBLMNTR3iaTOXJBn3fuCwf45zF_STN/view) | 4.65 GB | 2026-08-21 | Leave in inbox; not confidently tied to this batch |
| `Signal VS Noise.m4a` | [Open](https://drive.google.com/file/d/1ol7lkagbBQBhfU_ni9e4Vgh0NwgETYKL/view) | 17.15 MB | 2026-08-16 | Leave in inbox; audio could not be paired from available evidence |

## Simulated after state — what a full sweeper run would propose

This section is a proposal only. These names and paths were **not** written to Drive.

| Current file | Proposed new filename | Proposed destination | Confidence / blocker |
|---|---|---|---|
| `haz sales call.MP4` | `Chaz - Policy Approval and Frontloading - Raw.mp4` | `[Month filmed]/Sales Calls/Chaz - Policy Approval and Frontloading/` | High type confidence from transcript; filming month is not available, so the month folder is unresolved |
| `1` | `The Biggest Lie in Life Insurance - Raw.mp4` | `[Month filmed]/Scripted Talking Heads/The Biggest Lie in Life Insurance/` | High type confidence from transcript; filming month and duplicate/related-script check still required |
| `DJI_20260903130014_0007_D.MP4` | `[Video Name] - Raw.mp4` | `[Month filmed]/Scripted Talking Heads/[Video Name]/` | Visually appears to be scripted talking-head footage; exact script/title and filming month unresolved |
| `DJI_20260903124353_0006_D.MP4` | `[Video Name] - Raw.mp4` | `[Month filmed]/Scripted Talking Heads/[Video Name]/` | Visually appears to be scripted talking-head footage; exact script/title and filming month unresolved |
| 8 temporary MP4 files from August 21 | No proposed rename | Remain in `upload here` | Batch membership and relationship to an edit are not proven |
| `Signal VS Noise.m4a` | No proposed rename | Remain in `upload here` | No reliable pairing evidence |

### Important month-folder issue

The intended rule is **month filmed**, not month uploaded. The available Drive metadata gives upload/creation timestamps, but that is not proof of filming date. The existing [September 2026 folder](https://drive.google.com/drive/folders/11MCzFqqt8FA12VuYPTgT9OBEApIvS3BE) exists and contains `Scripted Talking Heads` and `Sales Calls`, but the sweeper must not use an empty folder or upload date as evidence of the correct route.

The existing September scripted folders are:

- `Recruiting Cycle`
- `Recognition`
- `The Lone Wolf`

The existing September `Sales Calls` folder is currently empty. That does **not** prove that a new upload is a sales call; in this dry run, the sales-call classification came from the transcript.

## After state — actual Drive state after this dry run

**Unchanged.** The upload inbox still contains the same 13 files with the same filenames and Drive file IDs. No folders were created, no files were renamed, and no files were moved.

## What this dry run tells us

The current sweeper is good at safely organizing known footage, but it stops before editing. In this inbox snapshot:

- One file is clearly a sales-call source that could later produce multiple clip-edit tasks.
- One file is clearly a scripted talking-head source.
- Two more files look like talking-head footage and are likely additional edit opportunities, but they need script/title confirmation before routing.
- The older temporary files are occupying the inbox and make automatic batch detection harder.

To turn this into more editing, the next downstream step would be clip selection and edit-task creation—especially for the sales call. This dry run intentionally did not create those tasks.

