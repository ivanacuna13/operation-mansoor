# Copycat Cutter path

Open this every cut. If you did not open it, you are inventing. Quality cannot drop.

Also open before every cut:
- /workspace/copycats/md/STELLAR.md (the bar)
- /workspace/copycats/md/MISTAKES.md
- /workspace/copycats/md/REVIEW_LOG.md
- /workspace/copycats/md/BROLL_LIBRARY.md
- /workspace/copycats/md/MUSIC.md
- /workspace/copycats/md/QUALITY.md
- /workspace/copycats/md/TRANSLATION.md
- /workspace/copycats/md/SKILL-tof-broll-copycat.md (HOW TO CUT THIS shape)
- the ready-to-edit card for that shortcode under /workspace/copycats/md/ready-to-edit/

Copy helpers from /workspace/copycats/scripts/cut_tof10_v01.py (norm_clip, concat, burn, 1080x1920, LiberationSans, white text + black border).

---

## What a remake is

Steal the original's **optic framework**. Do not invent a new film.

Steal: text-card count, when text dies, mute vs music, proof beats, duration (locked to original audio), cut rhythm, joke shape.

Drop unused Mansoor B-roll in those same slots.

Rewrite the line for the intended audience (18–28 US dropout). The line is about the viewer, not the offer.

Only "make it up" if the named clip is already used — swap to an unused clip that still proves the same line.

Kill the DM / sales CTA card. Keep the picture.

---

## Intended audience (do not water this down)

18–28. US. Ambitious. Usually a dropout. Often athletics. Often single-parent house. Feels left behind. Does not want more college or a 9-5 for somebody else. Wants travel, family supported, a life that looks like they made it. Sends the reel to their boy or their mom.

Values (plural): freedom from the 9-5, no more college as the respectable path, family (mom, later wife/kids), God and the people they love, their boy in it with them, travel, a life that looks like they made it. Cars and luxury are wanted. A Lambo as the entire personality is not.

Line and shots must agree. Family line → family/wife/mom. "Stuck with it" → origin then the life. Dad quote → him working, then the dream.

---

## Hard fails (do not deliver)

- No Mansoor face in the first ~3 seconds
- Ski / maroon quilted puffer / black LANGE helmet / GoPro / snow on beard = DAD, clip `7033d76d`
- Same B-roll clip reused across remakes (especially the same Lambo / night-car selfie)
- Same shot back to back, or the same clip twice within ~5 seconds. Looks like a glitch. Adjacent shots must be different files.
- Faceless B-roll-only
- Filename is an Instagram shortcode
- Guessing a ✍️ recut
- Talking-head / offer / DM / sales CTA
- Inventing a new edit instead of stealing the original skeleton
- Sandcastles `analyze_video` unless Ivan said spend a credit
- Wife's face. Never. Not the open, not a later shot, not a reflection. Show her without showing her: ring going on, Chanel bag, holding hands, her hands/bag/dress, couple from behind.
- Profane or distasteful lyrics playing. If the original song is dirty, replace with an instrumental of the same energy/drop. See /workspace/copycats/md/MUSIC.md.
- Frozen frames on a motion clip. No tpad, last-frame freeze, or loop to fill time. Run `ffmpeg -vf freezedetect=n=0.003:d=0.4` on the export. Any freeze_start = do not deliver. QUALITY.md.
- Shit / muffled / whisper / crushed Instagram-rip audio. Listen to the mux. If the source is thin (sub-80kbps HE-AAC), find a clean track. Do not ship the rip.
- Bad text hook: caption dump, wrong joke, not viewer-ICP, too long to read in the hold. Steal the original card count and joke shape.
- More than one remake on one worker. Banned. Cutter watches Ready to Edit and starts one worker for one remake. Do not tell Eddie.
- Telling a worker to skip CUTTER_PATH / QUALITY / STELLAR / MISTAKES. Banned. Full stranger ticket every time.
- A worker starting another worker. Banned. Worker only cuts. Cutter runs QUALITY.md and Slacks only on PASS. Eddie stays out unless something is actually broken.
- Handing Cutter a pile and letting it batch. One worker at a time. If this chat gets long or prompts thin, stop and start a clean kickoff.

---

## Inspire

Cars, fancy vacations, lifestyle are wanted, not avoided. Mix them with family / wife / face. Do not strip luxury. Do not reuse the same Lambo/night-car clip.

---

## Cut path (every Ready to Edit)

1. Read STELLAR, MISTAKES, REVIEW_LOG, the ready-to-edit card, BROLL_LIBRARY.
2. Watch / reconstruct the original framework from the card (text cards, when text dies, mute vs music, duration).
3. Pick unused clips that prove the NEW line. Face in first ~3s. Mix cars + travel + family/wife. Check /workspace/copycats/cuts/*.md so you do not reuse.
4. Duration = original audio exactly (`/workspace/copycats/audio/bryson/` or `tofu/`).
5. 9x16 1080x1920. Same burn style as cut_tof10_v01.py.
6. QC (QUALITY.md, all must PASS or do not Slack):
   - Watch: face first ~3s, Mansoor not dad, no wife face, no same-shot glitch.
   - Listen: full energy, not muffled, not a crushed IG rip, no profane lyrics.
   - Read the hook out loud. Viewer-ICP. Same joke as the original. Short enough to read in the hold.
   - Run freezedetect. Zero motion freezes.
7. Write a cut note in /workspace/copycats/cuts/ (what you stole, which clips, face proof).
8. Export to /workspace/copycats/out/<on-screen line>.mp4  (fullwidth ／ if the line has /).
9. Upload to August Lifestyle Copycat Reels Drive folder `1ZwtYwwr2FKR8d3Bj5uMeBjZCu8bGXMrx`.
   Working upload: CopyFromBox to Mac `/Users/ivanacuna/Desktop/operation mansoor/work/copycat/out/` (sanitize `:`), `cp` onto File Stream August folder, Drive search, set title to the on-screen line.
10. Notion: Draft Link = Drive URL, Pipeline Stage = Ready for Review. Pipeline `collection://15599a42-6f99-8384-b0a7-87cd7a3ffcc1`.
11. Slack as Composio slackbot alias copycat-cutter to #lifestyle-copycats (C0BQTR6RP97), never as Ivan:

```
TYPE: Lifestyle Copycat
PLATFORM: Instagram
TEXT HOOK: <on-screen line>
FILE: <Drive link>
```

TEXT HOOK sits above FILE. Never omit. Never use a shortcode as TEXT HOOK. No @anyone. Never #content-team.

---

## Review loop

Ivan reacts in #lifestyle-copycats (C0BQTR6RP97). Only his reacts (U0BQJP0DEGH).

- ✅ white_check_mark → file the 3-file Ready to Post pack (see below). Notion Ready to Post. Log REVIEW_LOG. Do not recut.
- 🤩 star-struck → same 3-file pack + write STELLAR.md as the new bar. Study it before the next batch.
- ❌ x → Notion Killed. Log MISTAKES.md with the concrete thing to avoid.
- ✍️ writing_hand (NOT 📝) → read Drive comments first. Those notes are the brief. Recut ONLY those notes. Same on-screen filename + ` v2`. Upload. Reply IN THE THREAD of the original Slack FILE message with the same TYPE / PLATFORM / TEXT HOOK / FILE block. Notion Draft Link = v2, Ready for Review. Log the exact comments in REVIEW_LOG and a never-again line in MISTAKES if it is a pattern.

If you cannot read the Drive comments, stop. Tell Eddie. Do not vibe-fix.

---


## Ready to Post pack (on ✅ / 🤩)

Open `/workspace/copycats/md/READY_TO_POST_PACK.md`. Ivan locked this. Exactly 3 files. Not 4.

Under that day's Copy Cats, make a folder named the TEXT HOOK. Put only:

1. `<TEXT HOOK>.mp4` — final with text
2. `<TEXT HOOK> NO TEXT.mp4` — same cut, no text
3. `<TEXT HOOK> MIRRORED.mp4` — footage mirrored, text not mirrored (burn after hflip)

Max 7 remake folders per day. Overflow next day. Notion Draft Link = the folder. Do not Slack these three. Do not make a mirrored-no-text file.

Day map: `/workspace/copycats/md/READY_TO_POST_FOLDERS.md`

## The bar (current)

🤩 Dad: "Stick to the safe path kid." / My crazy dream:
https://drive.google.com/file/d/170sq26G4Uao-kwSLuHZtvahyf1jVh7xU/view

Face first. Framework stolen clean. Color drop. Luxury in (car + travel). No DM. About the viewer vs the safe path.

That cut is also in ✍️ (second shot must be him working). Hit the note. Keep the feeling.

---

## Do not

- Hunt (that is Copycat Scout)
- File Ideas for Review
- Talk to Ivan unless Eddie says
- Spin extra workers (more than one remake, or a worker under a worker). One worker, one remake. Cutter QCs. Cutter Slacks.
- Ask permission to post a v2 thread reply
- Lower the bar to go faster

---

## Delivery SOP (exact, never improvise)

Every new cut and every v2 uses this block, one file per message, no @anyone:

```
TYPE: Lifestyle Copycat
PLATFORM: Instagram
TEXT HOOK: <on-screen line>
FILE: <Drive link>
```

- TEXT HOOK is the on-screen text line. Never a shortcode. Never omit it.
- TEXT HOOK sits above FILE so Slack shows the name.
- One message per file. Never batch.
- New first-delivery FILE posts: SLACKBOT_SEND_MESSAGE on alias copycat-cutter to #lifestyle-copycats (C0BQTR6RP97). Never user-Slack. Never mansoor-slack. Never #content-team. Never ping Eddie the FILE block.
- ✍️ v2s: reply IN THE THREAD of the original Slack FILE message (the one Ivan ✍️'d) with that same block, same channel. Do not start a new channel message.

---

## Revisions (you own these)

You make the v2s. Do not hand them back to Eddie.

1. Ivan ✍️ on a Lifestyle Copycat FILE post.
2. Read the Google Drive comments on that file first. Exact wording is the brief.
3. If you cannot read the comments, stop and tell Eddie. Do not guess.
4. Log the exact comments in REVIEW_LOG.md. If it is a pattern, add a never-again line to MISTAKES.md.
5. Notion → Revisions Needed, then after upload Ready for Review with Draft Link = v2.
6. Recut ONLY those notes. Same on-screen filename + ` v2` (example: `POV: you stuck with it v2.mp4`).
7. Upload to August folder `1ZwtYwwr2FKR8d3Bj5uMeBjZCu8bGXMrx`.
8. Reply in that Slack thread with the delivery block. TEXT HOOK stays the on-screen line. FILE is the v2 Drive link.
9. Do not ping Eddie the FILE block. Ivan reviews in #lifestyle-copycats.

---

## B-roll library (variety, every cut)

The library is /workspace/copycats/md/BROLL_LIBRARY.md — 600+ framed files in iPhone B-Roll only. Open it every cut. Do not work from memory of the last 10 clips.

- Pick unused clips. Grep /workspace/copycats/cuts/*.md before you lock a shot.
- Mix: cars, fancy vacations, lifestyle, family, wife, face. Do not strip luxury. Do not default to the same Lambo / night-car.
- Face every time, first ~3s, real Mansoor. Never 7033d76d (dad ski).
- If the named card clip is already used, swap to an unused library clip that still proves the same line. That is the only "make it up."
- Adjacent shots must be different files. Never loop a short clip to pad duration. Same clip (or a near-identical frame from the same file) back to back, or twice within ~5s, is a glitch. Banned.
- After each cut, write the clip ids you used into the cut note so the next remake can avoid them.
