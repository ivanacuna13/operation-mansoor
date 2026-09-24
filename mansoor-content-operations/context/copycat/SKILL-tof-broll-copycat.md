---
name: TOF B-roll copycat
description: >-
  Use when hunting or breaking down top-of-funnel B-roll copycat reels (music +
  text + lifestyle B-roll). Includes the translation layer for Mansoor's
  intended audience. Do not use for talking-head, podcast clips, narration
  stories, or product demos.
---
# TOF B-roll copycat

One job: find a remakeable reel, prove it, translate it for the intended audience, file the card. Open this skill every hunt. If you did not open it, you are inventing.

Also required: the translation page (`TRANSLATION.md`) and the music lock (`MUSIC.md`). If you file without the translation layer, the card is not ready to edit. Profane lyrics do not kill the idea — mark `MUSIC: clean` or `MUSIC: profane — Cutter must replace with instrumental`.

Funnel: Bryson Bowman, https://youtu.be/ScioHpkN9V8
Piles: Sandcastles Bryson `95f998ec-88e7-473d-9d3d-0134d5da9797` and Tofu `66b649f4-97ad-4d07-905b-32102f864559`
Notion: Copycat Pipeline `collection://15599a42-6f99-8384-b0a7-87cd7a3ffcc1`

```
trending / emotional audio
+ lifestyle B-roll
+ on-screen text about the viewer
= a reel someone sends to a friend
```

Usually 6–15s. Almost never a spoken hook. Face can appear. The video is not about the offer.

---

## Hard fails (read first)

- Talking-head, podcast, interview, narration vlog, how-to, numbered steps, live close, pep talk with no remakeable picture
- 80% of runtime is a face talking
- Theme-only search (`energy`, `mindset`, `leadership`, `framework`, `how to`, `close`)
- You stopped after two empty queries and called the well dry
- `analyze_video` unless Ivan said spend a credit
- Nested Task / executor / subagent
- Pipeline Stage set to Ready to Edit
- Dumping the fingerprint 63 into Notion
- Filing from a title without watching the file
- Filing without the translation layer (framework, original world, intended-audience values, new line, shots that prove that line)
- Line and shots do not agree (family line + empty car lot, "all yourself" as a sticker on a lone-wolf copy)
- A card whose Notes are a theme essay instead of HOW TO CUT THIS
- Calling the intended audience "Mansoor's guy." They are the intended audience / ICP. Be specific.
- Wife-face B-roll. Mansoor's wife's face never shows. Close-seconds only: ring, Chanel bag, holding hands, hands/bag/dress, couple from behind.
- Skipping a remakeable hit because the song is profane. Mark MUSIC: profane. File it.

A 1-second face into mute B-roll is fine. A recruit CTA on the last cards does not kill a TOF picture. Keep the picture. Drop the ask.

---

## 1. Find (Sandcastles)

Search matches captions, not pictures. Keep rotating queries until you have 5 remakeable B-roll reels or you can show a real try-map. Two empty phrases is not dry.

1. `ping`. If Sandcastles is down, stop and say so.
2. `list_items` on Bryson, then Tofu. Paginate. Skip filing any shortcode that already has a file in `copycat/bryson/` or `copycat/tofu/`. Use new items and the old handles/lines as seeds.
3. `channel_recap` on B-roll handles from those piles (e.g. solss.life). `lookback_days: 180`. New shortcodes only.
4. `search_my_videos` then `search_all_videos`: `platform: instagram`, `min_views: 100000`, `min_outlier_score: 2`, `lookback_days: 180`. If thin: 25k / 1.5x. Never below that.
5. Rotate query shapes. Do not quit because one was empty.
   - Short first-person lines from known winners, slightly rewritten
   - A known B-roll handle
   - Picture + line (`uncle kid car`, `night drive text`, `mom dad football`)
   - Other layers: family picked a smaller life / broke with the boy / opted out / they laughed at the job / will not lose to a text / they named you small / this night is the movie
6. If a query returns talking-heads, change the query. Do not file them.

**Kill before download.** Skip on title/caption: how to, step, lesson, framework, close, dm me, coaching, podcast, interview, 3 Es, process, outcome, mindset. Skip on thumbnail: face filling the frame in an office, car-seat talking, a mic. Keep: drive, night, family, plane, vacation, cars, work, with room for text.

`top_topics` is banned. `top_formats` is not a hunt. Do not add channels, projects, or items.

---

## 2. Watch and gate

Watch the file yourself. All five must pass or it dies.

1. **Share.** Name who the intended audience sends it to (their boy, their mom). If you cannot, skip.
2. **Picture.** Remake the first 3 seconds with Mansoor's B-roll in the same slots. Same text placement. Same cut rhythm. If no, skip.
3. **Library.** Name the slots: cars, family, planes, vacations, work, workouts, night. Not "he needs their Lambo."
4. **Audio.** The song has to carry the cut. Extract the real file. Listen for profanity / distasteful lyrics. Dirty vocals do **not** kill the idea — mark `MUSIC: profane — Cutter must replace with instrumental`. Clean = `MUSIC: clean`. See MUSIC.md.
5. **ICP.** Would the intended audience (18–28, US, dropout, left behind) send this to their boy or their mom? If the text is for a business owner, a coaching seeker, or a how-to, skip.

Viral bar on a wide search: 100k+ and 2× outlier, or 1M+. Pile items do not re-clear the bar.

### Ingest (only after the gate)

```
copycat/inbox/<handle>-<shortcode>/
  source.mp4
  audio.m4a
  SOURCE.md
```

```
ffmpeg -y -i source.mp4 -vn -acodec copy audio.m4a
```

Do not invent song titles. Do not paraphrase the on-screen line.

---

## 3. Translate (required, or do not file)

The original has a **framework** and a **world**. Steal the framework. Do not steal the original creator's world.

**Framework:** where the text sits, when it dies, the cut rhythm, the song, the joke shape.

**Original world:** their trophies, their insults, their idea of a good life (unpaid internship, two Lambos at 24, "I did it all myself").

**Intended audience:** 18–28, US, ambitious, usually a dropout, often athletics, often a single-parent house. Feels left behind. Does not want more college or a nine-to-five for somebody else. Wants money, a first Lambo, travel, to support family, to live on their own terms. Thinks they lack a system. Calls him Unc. Sends the reel to their boy or their mom.

**Their values (plural), from the interview:**
- Freedom from the nine-to-five. The safe job is the cage they are running from.
- No more college as the respectable path.
- Family: mom, the people they have to prove something to, later a wife and kids.
- God, and the people they love. Not lone-wolf guru.
- Their boy in it with them.
- Travel. Freedom to go.
- A life that looks like they made it. A Lambo is allowed. A Lambo as the entire personality is cringe influencer, which this is not.

Insurance looks small until the life proves it isn't.

**Translation** is: name the framework, then rewrite the line and pick the pictures so they prove the intended audience's values.

"Sure bro, go cop that unpaid internship" is not about internships. It is sarcasm that shoves the doubter back into the life *they* think is safe. For this audience that life is the secure 9-5 (and the degree that feeds it). Keep the shove. Change the cage.

A convertible and God in the same reel is fine when you chose it. It is wrong when the line says family and every shot is an empty car lot.

Pictures follow the line. Family line → family, friends, wife, mom. Running from a 9-5 → the night after, travel, the table with their people, a car they earned, on purpose. Do not default to Lambos because the original did.

If you only swap a noun, you missed it. If line and shots disagree, do not file.

Full page: `TRANSLATION.md`.

---

## 4. File

One Copycat Pipeline row per winner.

| Field | Value |
|---|---|
| Name | First on-screen line (original, so Ivan can match the link) |
| Pipeline Stage | Ideas for Review |
| Inspiration Link | Instagram URL |
| Notes | HOW TO CUT THIS (below) |
| Mansoor Footage | blank |
| Editor | blank |
| Draft Link | blank |

```
HOW TO CUT THIS
- Framework (what we steal): joke shape / hold / text placement / cut / song
- Original world: their insult, their trophy, their idea of a good life
- Intended audience values this remake proves: (name them)
- New line: exact on-screen text
- Shots that prove that line: which library slots, and why they match the line
- First 3 seconds: picture, text, placement
- Then: the cut this one actually does
- Song: energy + drop
- MUSIC: clean | profane — Cutter must replace with instrumental
- Layer + who they send it to (boy / mom)
- Do not: talking-head, offer, DM, lone-wolf sticker, Lambo-only when the line was about family
- Do not: wife-face (use ring / Chanel / hands / from behind)
```

Never Ready to Edit. That is Ivan.

---

## Receipt (required)

```
RECEIPT
- Skill opened: yes
- Translation page used: yes
- Queries tried: (list)
- Killed on title/thumbnail: N
- Watched: N (shortcodes)
- Filed: N (IG links)
- Why others died: one line each
```

Done = 5 Ideas for Review with the full Notes block (including translation), or a real try-map and 0. "Well is dry" after two phrases is a fail. A card without translation is a fail.

---

## Sheet (when ingesting)

```
# SHORTCODE — first on-screen text
- Source / handle / views / length / audio file
## Seven variables
## Framework / original world / intended-audience values / new line
## Text cards (exact words, in/out, placement)
## Frame by frame
## Library map (slots that prove the new line)
## Who they send it to
## Remake: first 3 seconds yes/no
```
