# Mastering Hooks | 10-16-25

- **Title:** Mastering Hooks | 10-16-25
- **Source filename:** Mastering Hooks | 10-16-25.mp4
- **Duration:** 39:35
- **STT engine:** onnx-asr / NVIDIA Parakeet TDT 0.6B v2 (int8) + Silero VAD
- **Date:** 2026-08-17

## Transcript

[00:00:00 – 00:00:00] That is
[00:00:02 – 00:00:03] The name sounds familiar.
[00:00:03 – 00:00:04] Yes.
[00:00:05 – 00:00:06] Oh no, okay.
[00:00:10 – 00:00:11] Black S DJ.
[00:00:12 – 00:00:14] Ah, yes.
[00:00:16 – 00:00:17] He's been the homie for a minute.
[00:00:18 – 00:00:21] Miami's just gotta be the spot friends of these Jays, huh?
[00:00:22 – 00:00:23] Dude, he lives in Ohio.
[00:00:26 – 00:00:27] He's an Ohio boy.
[00:00:27 – 00:00:29] You don't you don't even live in Miami.
[00:00:30 – 00:00:31] Oh wow.
[00:00:31 – 00:00:33] But he wants to move to my he's been trying to
[00:00:34 – 00:00:36] Get me to move in with him for ages'cause he just wants to
[00:00:36 – 00:00:38] market like hell, but
[00:00:39 – 00:00:40] I think it'll finally make sense.
[00:00:42 – 00:00:45] Like try it out for six months. I'm I'm weird about living with people, man.
[00:00:47 – 00:00:47] Me too.
[00:00:52 – 00:00:53] everything
[00:00:53 – 00:00:54] Quarterly.
[00:00:57 – 00:01:01] Nine ten at nine ten we're gonna rock and roll.
[00:01:01 – 00:01:02] We're going to open up
[00:01:02 – 00:01:03] with a
[00:01:04 – 00:01:04] Um
[00:01:05 – 00:01:10] QA session. QA session wanted to be directly about content. If you guys have any questions about.
[00:01:10 – 00:01:11] onboarding or anything like
[00:01:12 – 00:01:14] Throughout the program, you guys can contact us directly.
[00:01:14 – 00:01:15] Um
[00:01:16 – 00:01:17] But when it comes to
[00:01:17 – 00:01:18] Uh coach calls.
[00:01:19 – 00:01:21] We just want to talk about high level information and then
[00:01:22 – 00:01:25] After we go through all the questions that everyone has, we're gonna go through uh
[00:01:25 – 00:01:27] a really good training on hooks.
[00:01:28 – 00:01:29] And
[00:01:29 – 00:01:34] I guess understanding your brand and the way that that's going to influence the hook frameworks that we have.
[00:01:35 – 00:01:36] Don't.
[00:01:37 – 00:01:39] We have fun order one. Last time I gave this training.
[00:01:40 – 00:01:43] increased like the retention of
[00:01:43 – 00:01:44] A majority of the videos back.
[00:01:45 – 00:01:46] Literally, we were getting like 100.
[00:01:47 – 00:01:48] Fifty two hundred percent.
[00:01:48 – 00:01:49] View time videos.
[00:01:50 – 00:01:50] Um
[00:01:50 – 00:01:53] When we did that competition last time, I don't know if anyone in here.
[00:01:53 – 00:01:54] Who is it part of that?
[00:02:00 – 00:02:01] Yeah.
[00:02:04 – 00:02:05] That shit might kill me.
[00:02:06 – 00:02:07] That's really cool.
[00:02:09 – 00:02:10] Well
[00:02:14 – 00:02:14] Yeah.
[00:02:16 – 00:02:18] That was the worst chicken I've ever.
[00:02:18 – 00:02:19] ever had.
[00:02:20 – 00:02:22] That was actually uh remarkably bad.
[00:02:22 – 00:02:23] Bye.
[00:02:23 – 00:02:24] And on to
[00:02:24 – 00:02:26] Yeah, I've been checking out a bit.
[00:02:26 – 00:02:27] To port as
[00:02:27 – 00:02:28] Pop your uh
[00:02:29 – 00:02:30] Pop your cameras on, let's get rolling.
[00:02:31 – 00:02:36] I can't be I can't be looking at like blank screens dude it just weirds me out
[00:02:36 – 00:02:36] Check.
[00:02:36 – 00:02:37] Mm-hmm.
[00:02:37 – 00:02:38] Never ends.
[00:02:38 – 00:02:39] That will gauge.
[00:02:39 – 00:02:41] Everything.
[00:02:42 – 00:02:42] Mm.
[00:02:42 – 00:02:44] Mine's gonna be black, right, so I'm driving.
[00:02:45 – 00:02:49] That's okay. Marcos hit me up and told me to get on it's for the uh
[00:02:50 – 00:02:51] Or add some shit.
[00:02:52 – 00:02:53] I'll do him a favor.
[00:02:55 – 00:02:56] Alright.
[00:02:57 – 00:02:58] Boys, let's rock and roll.
[00:03:00 – 00:03:00] Yeah.
[00:03:00 – 00:03:01] What's going on, y'all?
[00:03:02 – 00:03:04] So today, like I said, we're going to be talking about
[00:03:05 – 00:03:05] Um
[00:03:06 – 00:03:07] Hooks.
[00:03:07 – 00:03:08] primary thing.
[00:03:08 – 00:03:09] Especially when getting started.
[00:03:10 – 00:03:11] with social media. Now
[00:03:11 – 00:03:13] I've got a hard stop.
[00:03:13 – 00:03:17] in about 49 minutes, so I'm going to fly through this.
[00:03:17 – 00:03:18] Um
[00:03:18 – 00:03:20] If you have any questions, put them into the chat.
[00:03:21 – 00:03:24] And I will answer them the second that I'm done.
[00:03:25 – 00:03:26] That being said,
[00:03:27 – 00:03:28] What do we have in here?
[00:03:29 – 00:03:29] Right.
[00:03:29 – 00:03:29] Mm-hmm.
[00:03:30 – 00:03:30] Yes, I had
[00:03:30 – 00:03:32] I send a reminder super late.
[00:03:32 – 00:03:35] Okay, so uh little housekeeping business stuff. So number one.
[00:03:37 – 00:03:37] Um
[00:03:38 – 00:03:41] Currently working heavily on
[00:03:41 – 00:03:43] A completely new S O P
[00:03:43 – 00:03:47] And module that's going to be really big for every single person in here.
[00:03:47 – 00:03:48] And it is
[00:03:48 – 00:03:49] Turning
[00:03:49 – 00:03:50] Sales calls.
[00:03:50 – 00:03:51] into content.
[00:03:52 – 00:03:55] So I know a lot of you guys that are in here, especially in the insured space.
[00:03:55 – 00:04:03] Wanted to make content, but are busy at the same time. One of the biggest trust assets that we have is literally what we do.
[00:04:03 – 00:04:04] Or works.
[00:04:04 – 00:04:09] And just being able to document it properly to retain viewers, to stop the scroll.
[00:04:09 – 00:04:10] Um and to convert.
[00:04:10 – 00:04:14] That is what I am working on right now. We're almost done with it.
[00:04:14 – 00:04:21] The video dude, my editor's in there, it's like a three-hour and 50-minute video that I told him to cut down to like 35 minutes. So he's frying through that right now and then.
[00:04:21 – 00:04:25] I'm personally working on the SOP, so the standard operating procedure.
[00:04:25 – 00:04:27] breaking down every
[00:04:27 – 00:04:33] Style every version and then the lookalike videos and the reference videos that you guys can use when recreating your own.
[00:04:33 – 00:04:34] Um as well.
[00:04:35 – 00:04:38] That's what we're working on, so be looking for that within the next week.
[00:04:39 – 00:04:39] Dropping.
[00:04:39 – 00:04:40] Um
[00:04:41 – 00:04:45] And then before we get into it, just wanted to open up with any questions that you guys have.
[00:04:53 – 00:04:54] No questions?
[00:04:56 – 00:04:57] That makes it easy on me.
[00:04:58 – 00:04:58] Well
[00:04:59 – 00:05:00] So
[00:05:00 – 00:05:01] Where'd it pop open? So.
[00:05:02 – 00:05:02] With
[00:05:02 – 00:05:03] Hux, can anyone
[00:05:04 – 00:05:08] Tell me the time frame that you have for a hook on a short form video.
[00:05:11 – 00:05:11] You got like
[00:05:12 – 00:05:14] three s first three or four seconds of people are gone.
[00:05:15 – 00:05:16] Yeah, a couple seconds.
[00:05:16 – 00:05:17] Yeah, you have a couple seconds.
[00:05:18 – 00:05:22] And there's arguments about the actual amount of time that it is.
[00:05:22 – 00:05:27] Uh and it and it really has to do with so many variable factors.
[00:05:27 – 00:05:31] Um some of them are subconscious and some of them are conscious. So
[00:05:31 – 00:05:32] Within that.
[00:05:32 – 00:05:40] I usually say the first two second block. That's the rule of thumb. Because if I set the expectation as two seconds and you try to fit everything into two seconds,
[00:05:41 – 00:05:43] Even if you go over a little bit, you have some
[00:05:44 – 00:05:45] Room for grace.
[00:05:45 – 00:05:46] Um
[00:05:46 – 00:05:49] But yeah, we're we're we're in an attention war.
[00:05:49 – 00:05:53] And we're basically fighting for the attention of people with nat brains.
[00:05:53 – 00:05:55] Scrolling on videos.
[00:05:55 – 00:05:57] Very, very fast, consuming content.
[00:05:57 – 00:06:03] And there's a lot of content there, and there's always something better in the viewer's mind.
[00:06:03 – 00:06:06] To get somebody to stop, there's three types of
[00:06:06 – 00:06:08] Hooks. I guess there's really four types of hooks.
[00:06:08 – 00:06:12] Um but some people argue one of them to be similar or the same.
[00:06:12 – 00:06:14] Anybody know what the four types of fucks are?
[00:06:21 – 00:06:21] Mm.
[00:06:23 – 00:06:27] Dude, I love doing this, just opening it up, waiting for somebody to say something nobody ever does.
[00:06:27 – 00:06:29] Come on, guys, you guys do sales, you're boss.
[00:06:29 – 00:06:30] So we have
[00:06:31 – 00:06:32] A
[00:06:32 – 00:06:33] Herbal hook.
[00:06:33 – 00:06:39] A verbal hook, there are literally hundreds, maybe a thousand ways to do a verbal hook.
[00:06:39 – 00:06:41] But it is the hook that you do with your voice.
[00:06:42 – 00:06:44] Um the the best way to really
[00:06:44 – 00:06:46] hack attention with a verbal hook.
[00:06:46 – 00:06:49] is to do comparisons or
[00:06:50 – 00:06:51] Um
[00:06:51 – 00:06:52] But comparisons are at least
[00:06:52 – 00:06:54] My favorite. You can say things that are very
[00:06:54 – 00:06:55] Polar
[00:06:55 – 00:06:59] There's a lot of one-liners that you can do. I remember back in 2023,
[00:06:59 – 00:07:01] I started using I hate.
[00:07:03 – 00:07:11] Just as the first two words of every single video that I did, and they just started ripping multiple hundred thousand views, selfie talking videos over and over and over again.
[00:07:11 – 00:07:11] Um
[00:07:12 – 00:07:13] So the hook frameworks
[00:07:14 – 00:07:16] We're also dropping a night. I was doing some revamps.
[00:07:16 – 00:07:17] Do it.
[00:07:17 – 00:07:18] Um
[00:07:18 – 00:07:21] But I'll drop you guys the hook frameworks tonight as far as
[00:07:21 – 00:07:23] Like the actual way that you plug in
[00:07:24 – 00:07:25] Uh.
[00:07:25 – 00:07:33] The building blocks of a hook. It's like you can just plug in whatever industry you're in, whatever number of earnings it's talking about in the hook.
[00:07:33 – 00:07:37] Can actually give you guys a couple examples really quick because we're almost done with this thing.
[00:07:37 – 00:07:39] Um let me pull this up.
[00:07:39 – 00:07:45] And then the viral video strategies SOP that you guys got sent to you also has a bunch on there. But the one that I'm dropping.
[00:07:45 – 00:07:46] As I can
[00:07:47 – 00:07:47] Hundreds.
[00:07:48 – 00:07:50] Um let me pull this up really quick.
[00:07:52 – 00:07:59] But while I'm looking for this, the verbal hooks is just what you are saying out loud to stop the scroll, to get the person to watch.
[00:07:59 – 00:08:01] Um controversy
[00:08:02 – 00:08:05] Polar hot takes are really good.
[00:08:06 – 00:08:07] Large amounts of money.
[00:08:07 – 00:08:08] And then
[00:08:09 – 00:08:14] Also, the influx in your voice and actually the way that you say it, the tempo at which you say it is also important when doing.
[00:08:14 – 00:08:16] A verbal hook.
[00:08:16 – 00:08:16] Okay.
[00:08:16 – 00:08:17] Um
[00:08:18 – 00:08:18] Yeah, another one.
[00:08:19 – 00:08:24] Think or one thing could be like: the mistake I see new entrepreneurs make is.
[00:08:24 – 00:08:25] Um
[00:08:26 – 00:08:28] Here's a business act that's so effective, it feels like cheating.
[00:08:29 – 00:08:36] Stop grinding 80 hours a week. Do this instead. Three books that taught me more about business than my MBA. Okay. And it goes on and on and on and on and on and on and on.
[00:08:37 – 00:08:38] Okay, so we'll be cooking in that.
[00:08:38 – 00:08:39] Um
[00:08:39 – 00:08:42] Next one. Can anyone guess what the next one is? Verbal's already out of the way.
[00:08:47 – 00:08:48] It's like the easiest one.
[00:08:49 – 00:08:50] And it's the most influential.
[00:08:51 – 00:08:52] What did you say?
[00:08:53 – 00:08:54] Is this sure?
[00:08:54 – 00:08:54] Visual.
[00:08:55 – 00:08:56] Yes.
[00:08:56 – 00:08:57] Visual hooks.
[00:08:57 – 00:09:00] A visual hook um it's actually the
[00:09:00 – 00:09:00] Uh
[00:09:01 – 00:09:03] Reference that I use.
[00:09:03 – 00:09:05] is from a video that I made as a joke.
[00:09:06 – 00:09:08] Like I was literally making the video.
[00:09:09 – 00:09:12] On a coaching call, and then I went and posted it on trial rails, but I made it.
[00:09:12 – 00:09:14] To just show.
[00:09:15 – 00:09:16] The the guy that I was coaching, like
[00:09:17 – 00:09:19] The concept of what I was talking about.
[00:09:20 – 00:09:25] And it ended up doing like 700,000 views. It was so stupid. It was a video where I held up.
[00:09:25 – 00:09:26] This uh
[00:09:26 – 00:09:27] This toothbrush pack.
[00:09:28 – 00:09:32] I literally held it up to the screen, it was in focus for about two seconds, and then I pulled it back.
[00:09:32 – 00:09:33] That's
[00:09:33 – 00:09:34] All it was.
[00:09:34 – 00:09:36] And it ripped like 700K.
[00:09:36 – 00:09:37] Um
[00:09:37 – 00:09:39] For the purpose of this, I actually can uh
[00:09:39 – 00:09:44] But while I'm while I'm pulling up this video of the visual hook, can anyone guess the last
[00:09:44 – 00:09:45] Two. There's two more.
[00:09:54 – 00:09:55] I'm pulling. You got shock factor?
[00:09:57 – 00:09:59] Shock factor is uh
[00:10:01 – 00:10:05] It's not one of the four categories of hooks. It's more of a
[00:10:06 – 00:10:07] Eight.
[00:10:07 – 00:10:08] Product.
[00:10:08 – 00:10:09] of the hook itself.
[00:10:10 – 00:10:12] If that makes sense.
[00:10:12 – 00:10:14] I could cause shock factor.
[00:10:14 – 00:10:16] with a verbal hook.
[00:10:16 – 00:10:17] or a visual hook.
[00:10:17 – 00:10:24] I mean shock factor could be like if I just had my cock wide out on Instagram and they landed on that, that's shock factor.
[00:10:24 – 00:10:26] Okay, that's a visual hook.
[00:10:27 – 00:10:33] Versus if I had verbal hook and I said something incredibly racist or anti-Semitic or something just
[00:10:33 – 00:10:34] Insane.
[00:10:35 – 00:10:37] That still provides you shock factor.
[00:10:38 – 00:10:41] And I did it verbally versus visually.
[00:10:42 – 00:10:44] Very extreme examples, but it
[00:10:44 – 00:10:46] Helps for the purpose of teaching. Does that make sense, Damien?
[00:10:49 – 00:10:50] Yeah, that makes sense. Yep. So
[00:10:51 – 00:10:56] Um, let me pull this video up though. I wanted to show you guys a visual hook because I had a verbal hook and a visual hook at the same time.
[00:10:57 – 00:11:04] It's the it wasn't really a verbal hook, but it's a visual hook. Okay. Oh, it has 1.4 million views now. I have no idea how that happened.
[00:11:05 – 00:11:05] Um
[00:11:06 – 00:11:10] Let me share my screen, I'll share sound too, optimize for video sharing.
[00:11:11 – 00:11:13] Can you guys see this?
[00:11:16 – 00:11:17] You guys see this, okay?
[00:11:18 – 00:11:18] Right.
[00:11:18 – 00:11:20] So let me see here, where is that video at?
[00:11:21 – 00:11:23] Uh oh I lost it. I had it and now it's gone.
[00:11:24 – 00:11:25] Um is it up or down? Okay, right here.
[00:11:26 – 00:11:29] Okay, they say he did 1.4 million views. And I just want you to notice.
[00:11:30 – 00:11:32] How fast the visual hook happens.
[00:11:33 – 00:11:36] Where your eyes immediately go on the video.
[00:11:37 – 00:11:39] And then what I say to support
[00:11:39 – 00:11:40] Fort.
[00:11:40 – 00:11:41] The visual hook.
[00:11:47 – 00:11:47] Think?
[00:11:48 – 00:11:50] are$40 a half.
[00:11:50 – 00:11:51] So that's how you get
[00:11:52 – 00:11:54] It literally is like
[00:11:54 – 00:11:54] Bro, yeah.
[00:11:55 – 00:11:55] So this?
[00:11:56 – 00:11:56] Thanks.
[00:11:57 – 00:11:57] 'Kay.
[00:11:58 – 00:12:02] Grow these little things. How fast did that happen? And then we're already in focus.
[00:12:02 – 00:12:06] So it's the visual and the verbal, but there's also another type of hook on this video.
[00:12:06 – 00:12:08] I don't personally count it as a hook.
[00:12:08 – 00:12:11] But some other large brand creators and stuff
[00:12:11 – 00:12:12] Do, um
[00:12:13 – 00:12:15] I don't know. I I I just don't really think it's a
[00:12:15 – 00:12:16] Totally a huckboat.
[00:12:17 – 00:12:20] Can you guys guess what the third hook that's happening on this video is right now?
[00:12:24 – 00:12:25] car you're in.
[00:12:26 – 00:12:26] No.
[00:12:27 – 00:12:37] But that would that would still fall under vis that would that would still fall under visual, but that is a good point. There's a level of confusion for me, like why is this dude talking about toothpaste or toothbrushes?
[00:12:38 – 00:12:41] So that is that is the beauty of a video book.
[00:12:41 – 00:12:42] Is it is a
[00:12:43 – 00:12:44] Again, these are products.
[00:12:45 – 00:12:46] Oh.
[00:12:46 – 00:12:49] The hooks themselves. These are these are products.
[00:12:50 – 00:12:51] of doing
[00:12:51 – 00:12:52] The visual hook.
[00:12:52 – 00:12:53] or the verbal hook.
[00:12:54 – 00:12:59] You then feel curious if I do it correctly. It incites an emotion. That's what a hook is supposed to do.
[00:12:59 – 00:13:01] It's supposed to incite some type of emotion.
[00:13:02 – 00:13:04] Okay, so if I if you're saying
[00:13:04 – 00:13:06] You know, curiosity, that means I did a good job.
[00:13:07 – 00:13:10] My hook framework worked well, okay? But it's a caption.
[00:13:10 – 00:13:11] Huck.
[00:13:11 – 00:13:12] Yeah, I see these like
[00:13:13 – 00:13:13] Am I
[00:13:13 – 00:13:16] Editors were doing these fancy little captions. I have videos on
[00:13:16 – 00:13:19] Other program on how to do those too. But it's a caption hook.
[00:13:19 – 00:13:22] Personally, I don't think that's really a hook.
[00:13:22 – 00:13:24] The type of hook that I do think
[00:13:24 – 00:13:26] is actually a hook would be a
[00:13:26 – 00:13:27] Title
[00:13:27 – 00:13:27] Fuck.
[00:13:28 – 00:13:28] Right here.
[00:13:29 – 00:13:31] This is a title hook. So caption hooks.
[00:13:31 – 00:13:33] Go under the chin.
[00:13:34 – 00:13:35] Title hooks.
[00:13:35 – 00:13:35] Go.
[00:13:36 – 00:13:38] Like right under where the uh
[00:13:38 – 00:13:40] On Instagram, like the little
[00:13:40 – 00:13:42] thing that's on the top of the screen is that.
[00:13:43 – 00:13:44] Yeah.
[00:13:44 – 00:13:45] Title hooks.
[00:13:46 – 00:13:49] Visual hooks, verbal hooks, and then you have caption, which I
[00:13:50 – 00:13:54] will argue till the day I die that it's not really a hook. Nothing really hooks me about a caption itself.
[00:13:54 – 00:13:55] Um
[00:13:55 – 00:13:56] I guess if they weren't
[00:13:56 – 00:13:58] L if they were listening without audio it might work.
[00:13:59 – 00:13:59] Yeah.
[00:14:00 – 00:14:02] So with those four different types of hooks.
[00:14:03 – 00:14:05] If you are creating a video.
[00:14:06 – 00:14:08] If you are coming up with an idea.
[00:14:08 – 00:14:10] Um if you're gonna talk about a topic.
[00:14:12 – 00:14:14] I literally can't stress enough.
[00:14:15 – 00:14:16] And I do this myself.
[00:14:17 – 00:14:17] all the time.
[00:14:18 – 00:14:19] is
[00:14:19 – 00:14:20] How
[00:14:20 – 00:14:21] Dumb.
[00:14:21 – 00:14:28] It is to focus on a video and put time into a video that nobody is going to watch.
[00:14:30 – 00:14:39] And the way that you can clearly indicate if somebody is going to watch your video or not is how engaging and how many of the hooks do I have.
[00:14:39 – 00:14:42] in the first couple of seconds, preferably two.
[00:14:43 – 00:14:45] That is like the make it or break it, meaning.
[00:14:46 – 00:14:48] If it takes you four seconds.
[00:14:49 – 00:14:53] to or four, five, six seconds to get out your your your sentence.
[00:14:53 – 00:14:57] The thing that's going to incite curiosity, incite some type of emotion.
[00:14:57 – 00:15:00] then people aren't going to watch it. One th
[00:15:00 – 00:15:01] One thing that I will do.
[00:15:02 – 00:15:03] Is with Hux.
[00:15:03 – 00:15:05] Verbally, you need to try to talk faster.
[00:15:06 – 00:15:07] 'Kay.
[00:15:07 – 00:15:08] Uh if it's a title hook.
[00:15:08 – 00:15:11] You need to, if you have it like super wordy.
[00:15:11 – 00:15:16] Guess what you need to do? Dumb it down to where a third grader could read it.
[00:15:16 – 00:15:20] Make it the most simple title hook that you possibly can.
[00:15:20 – 00:15:21] While still
[00:15:21 – 00:15:23] giving them the message of what the video is going to be about.
[00:15:23 – 00:15:24] Yeah.
[00:15:24 – 00:15:28] We use title hooks for foreshadowing. Same with visual hooks. Everything's pretty much just.
[00:15:29 – 00:15:30] It's letting the viewer know.
[00:15:31 – 00:15:33] One, stop scrolling.
[00:15:33 – 00:15:36] And two, here's what you're gonna get if you stay.
[00:15:38 – 00:15:39] Does that make sense?
[00:15:42 – 00:15:46] But if if a viewer doesn't know what that is, okay, if a viewer doesn't know what like the
[00:15:47 – 00:15:49] Why they're staying on the video.
[00:15:50 – 00:15:50] Or
[00:15:51 – 00:15:56] Like they don't know what the video's gonna be about and they don't know why they're staying on the video. They're not.
[00:15:56 – 00:15:59] Going to, and they're definitely not if it takes you.
[00:15:59 – 00:16:02] five seconds to get the fucking point across.
[00:16:03 – 00:16:04] It's just
[00:16:04 – 00:16:08] How it goes at the end of the day. And I go back through my videos and I
[00:16:08 – 00:16:10] I'll have a four or five second
[00:16:12 – 00:16:12] Intro.
[00:16:13 – 00:16:14] But it'll be so good.
[00:16:16 – 00:16:19] And I'm just like, nope, this is the one. This is the one that breaks the rule.
[00:16:20 – 00:16:26] Like, this is just fire. It's got a. I've got the title hook. It's perfect. The copy's amazing.
[00:16:26 – 00:16:28] I've got the verbal hook, it's amazing.
[00:16:28 – 00:16:32] It like I've got the visuals, everything is amazing. It just takes a little bit too long.
[00:16:32 – 00:16:34] But it's still gonna work.
[00:16:35 – 00:16:35] It
[00:16:35 – 00:16:37] literally never works.
[00:16:39 – 00:16:40] The first
[00:16:40 – 00:16:42] Two to four seconds are
[00:16:43 – 00:16:45] All you should focus on.
[00:16:45 – 00:16:47] if you are really getting into content creation.
[00:16:48 – 00:16:52] And until you're hitting videos that are doing tens of thousands to millions of views.
[00:16:52 – 00:16:53] That is
[00:16:53 – 00:16:55] all you really need to focus on.
[00:16:56 – 00:16:57] Don't skip ahead.
[00:16:57 – 00:16:58] Now if you're doing paid traffic.
[00:17:00 – 00:17:01] With paid traffic.
[00:17:01 – 00:17:02] Bill Hawk.
[00:17:02 – 00:17:03] is a little bit
[00:17:03 – 00:17:04] Different.
[00:17:05 – 00:17:09] I guess the rules of the hook, the two to four second thing, that that stays consistent.
[00:17:10 – 00:17:13] But with the Andromeda update, can anyone guess?
[00:17:14 – 00:17:15] What is different?
[00:17:16 – 00:17:16] About
[00:17:16 – 00:17:17] Ads
[00:17:18 – 00:17:19] Versus
[00:17:19 – 00:17:21] like normal organic viral content.
[00:17:28 – 00:17:31] Can't get it right, it's okay. It's a is a little bit of a tough question.
[00:17:32 – 00:17:34] Basically with the Andromeda update.
[00:17:36 – 00:17:37] Andromeda
[00:17:37 – 00:17:40] I I don't wanna get like too deep'cause I don't wanna over confuse you guys, but basically it's
[00:17:41 – 00:17:42] Instead of
[00:17:43 – 00:17:44] trying to like
[00:17:44 – 00:17:46] Really hook in?
[00:17:46 – 00:17:48] As broad of an audience as possible in the beginning.
[00:17:50 – 00:17:52] What you're doing instead is you're trying to speak.
[00:17:53 – 00:17:56] directly to a certain person.
[00:17:56 – 00:17:58] and a certain pain point.
[00:17:58 – 00:18:00] as fast as possible.
[00:18:02 – 00:18:02] So
[00:18:02 – 00:18:03] For example,
[00:18:03 – 00:18:07] Um a couple of ads I had just cooked up actually.
[00:18:07 – 00:18:08] I've
[00:18:08 – 00:18:09] I cooked up a lot for
[00:18:10 – 00:18:13] Logan and Marcos too. Let me pop some of these open really quick.
[00:18:13 – 00:18:16] I was just at a mastermind with Jeremy Haynes. He does like$12 million a month.
[00:18:16 – 00:18:18] Ridiculous in it.
[00:18:18 – 00:18:21] in different offers through ads.
[00:18:21 – 00:18:22] But the
[00:18:22 – 00:18:24] The ad copy that I had.
[00:18:24 – 00:18:26] Came up with. Let me see here.
[00:18:27 – 00:18:28] Is
[00:18:29 – 00:18:30] Check.
[00:18:32 – 00:18:35] If you've made over 60K in sales and want to double your sales team.
[00:18:38 – 00:18:40] Okay, that that itself.
[00:18:40 – 00:18:44] is is probably not the best organic in the world.
[00:18:45 – 00:18:46] by any means.
[00:18:47 – 00:18:48] But it speaks.
[00:18:48 – 00:18:51] directly to a certain
[00:18:51 – 00:18:52] Percept.
[00:18:52 – 00:18:54] Which paid traffic
[00:18:54 – 00:18:57] For training your your pixel is what it's called. It's like the
[00:18:57 – 00:18:59] data set that basically
[00:18:59 – 00:19:01] helps meta identify
[00:19:01 – 00:19:03] Who to send your videos to?
[00:19:04 – 00:19:06] You want to train your data set.
[00:19:06 – 00:19:07] to send it out.
[00:19:08 – 00:19:08] Two people.
[00:19:09 – 00:19:12] by using the first two to four seconds.
[00:19:12 – 00:19:15] to clearly speak to exactly that person.
[00:19:16 – 00:19:17] So I've another one. Um
[00:19:18 – 00:19:20] If you're ready to scale your sales team,
[00:19:20 – 00:19:22] But shoulder tapping and cold outreach feels like a waste of time.
[00:19:24 – 00:19:25] So I speak.
[00:19:25 – 00:19:27] to the person and what they want.
[00:19:28 – 00:19:30] And then I speak to their pain point.
[00:19:31 – 00:19:32] Again.
[00:19:32 – 00:19:37] Ads are different than organic. So if you plan on running ads.
[00:19:38 – 00:19:42] The way that you set up your hooks is going to be a different ballgame.
[00:19:42 – 00:19:42] Um
[00:19:43 – 00:19:46] Then I've got like, if you haven't 5x'd your sales team in the past 12 months.
[00:19:47 – 00:19:47] 'Kay.
[00:19:48 – 00:19:51] If you guys noticed, almost every single person on this call.
[00:19:53 – 00:19:55] Falls directly under.
[00:19:55 – 00:19:57] The hooks that I just read off.
[00:20:00 – 00:20:05] You train your algorithm to go to your exact ICP.
[00:20:05 – 00:20:07] You train the metapixel.
[00:20:07 – 00:20:10] to target your ICP, your ideal client profile.
[00:20:10 – 00:20:12] Okay, I don't want to talk about
[00:20:12 – 00:20:18] On the ads, too much because that's a pretty plug and play. It's like that's that's really the key concept that you need to understand.
[00:20:18 – 00:20:19] Is just number one.
[00:20:20 – 00:20:21] If we're talking about hooks.
[00:20:22 – 00:20:23] You are speaking to the exact person.
[00:20:24 – 00:20:25] And
[00:20:25 – 00:20:28] the exact pain point as fast as possible.
[00:20:28 – 00:20:29] 'Kay.
[00:20:29 – 00:20:30] But then
[00:20:30 – 00:20:31] You can add in a visual hook.
[00:20:32 – 00:20:32] You can
[00:20:33 – 00:20:33] I mean the verbal hook.
[00:20:34 – 00:20:35] Is kind of like its own thing.
[00:20:36 – 00:20:36] Um
[00:20:37 – 00:20:39] I don't ever use title hooks, really.
[00:20:39 – 00:20:40] on ads ever.
[00:20:41 – 00:20:43] I do typically use caption hooks.
[00:20:43 – 00:20:44] Um
[00:20:44 – 00:20:45] So I use caption.
[00:20:45 – 00:20:46] And then I'll
[00:20:46 – 00:20:47] Speak to the
[00:20:48 – 00:20:49] Exactly I CP.
[00:20:49 – 00:20:52] Then I'll talk about the pain point all as fast as possible and occasionally use
[00:20:53 – 00:20:54] A visual hook as well.
[00:20:54 – 00:20:56] Usually the visual hook is done in the editing.
[00:20:57 – 00:20:58] In this
[00:20:59 – 00:21:02] from the subject, the person that's actually in the video talking to the camera.
[00:21:03 – 00:21:05] So um as you guys know as well.
[00:21:05 – 00:21:06] We have
[00:21:06 – 00:21:09] internal editors. You don't have to pay for like an editing service. We dropped that.
[00:21:10 – 00:21:12] Um but we do have editors that specifically do
[00:21:13 – 00:21:14] So if you guys ever do want ads, it's like
[00:21:15 – 00:21:16] 20 bucks a video.
[00:21:16 – 00:21:17] to get an ad done.
[00:21:18 – 00:21:18] So
[00:21:18 – 00:21:21] And they'll look just like the ones that you guys have probably seen.
[00:21:21 – 00:21:23] religiously since I started running them.
[00:21:23 – 00:21:24] Um
[00:21:24 – 00:21:25] So they're they're pretty good.
[00:21:26 – 00:21:29] So far, talking about ads and organic, does anyone have any questions?
[00:21:35 – 00:21:36] Somebody's gotta hit me with something, dude.
[00:21:37 – 00:21:38] Can we do an aga?
[00:21:39 – 00:21:47] Let me let me run something. Let me run something at you. So when you're doing like a hook, right? Like talking hooks, what's the
[00:21:47 – 00:21:51] best way to quality check it. So like obviously with like, you know
[00:21:52 – 00:21:55] Well no no no of course like obviously but I'm saying like
[00:21:55 – 00:22:00] You know, when you're going through the video checklist and you're being like, okay, we're here, here, here, we've done all this.
[00:22:00 – 00:22:02] Right. When you do like a basic edit.
[00:22:02 – 00:22:05] It's pretty clear, it either catches your attention or you doesn't.
[00:22:05 – 00:22:11] But when you're talking and you're viewing it yourself, it's a little bit different because you're looking at yourself talking.
[00:22:11 – 00:22:13] And you're gonna give yourself usually a little bit more.
[00:22:13 – 00:22:14] You know, leeway.
[00:22:15 – 00:22:17] or look towards it.
[00:22:17 – 00:22:21] ensure that your hooks when you're doing talking videos
[00:22:21 – 00:22:21] Or
[00:22:22 – 00:22:23] or pop it, you know.
[00:22:23 – 00:22:24] Um
[00:22:26 – 00:22:28] I I would still say trial reels method.
[00:22:28 – 00:22:31] I I think that it's almost impossible to get rid of
[00:22:32 – 00:22:33] your subjective bias toward
[00:22:34 – 00:22:35] Yourself.
[00:22:35 – 00:22:36] talking to the camera.
[00:22:37 – 00:22:40] And that's why I like the trial reels method is so cracked.
[00:22:40 – 00:22:42] is because
[00:22:42 – 00:22:44] You can literally do
[00:22:45 – 00:22:47] It's kind of like running ads before the Andromeda update.
[00:22:48 – 00:22:52] It's like you can have the same body of the video and the same CTA.
[00:22:53 – 00:22:55] And literally just try like
[00:22:55 – 00:22:58] five or ten different hooks and five or ten different titles.
[00:22:59 – 00:23:04] and see which one performs the best and then make that the winner and put it onto your primary page.
[00:23:04 – 00:23:05] Um
[00:23:05 – 00:23:05] Huh.
[00:23:06 – 00:23:08] That that that that's like straight up.
[00:23:08 – 00:23:14] The easiest way to do it is just sheer volume because anything aside from that is typically going to be subjective.
[00:23:15 – 00:23:17] It's going to be based off the person watching it.
[00:23:17 – 00:23:18] Um
[00:23:18 – 00:23:23] The one thing I would say is if you are gonna change variables, change as few as possible when you're doing the trial rails method.
[00:23:24 – 00:23:24] And
[00:23:24 – 00:23:26] Motion is always good.
[00:23:27 – 00:23:30] Motion in the first two seconds is always good.
[00:23:31 – 00:23:33] on the viral video strategies SOP.
[00:23:33 – 00:23:34] It talks about like
[00:23:34 – 00:23:37] the extreme contrast method and then having like
[00:23:37 – 00:23:44] Crazy objects in the background that can work pretty well. Like, again, these are just like visual things that you can put into the first two to four seconds.
[00:23:45 – 00:23:46] Bye.
[00:23:46 – 00:23:51] Overall, I would just say the the trial rails method is the number one way to test.
[00:23:51 – 00:23:54] Pretty much anything. And while we're talking on that,
[00:23:54 – 00:23:56] I will drop the trial reels method.
[00:23:57 – 00:24:05] SOP, this is just a PDF. I'm dropping it in here right now. We updated this, so I would definitely download this, guys. This has been recently updated.
[00:24:06 – 00:24:08] It's basically like
[00:24:08 – 00:24:10] Core idea is to, um
[00:24:11 – 00:24:12] Test.
[00:24:12 – 00:24:20] Basically, changing one thing. Find out what works in videos by testing small clear differences on jar reels before posting it to your main page.
[00:24:21 – 00:24:29] It's the key thing that I teach people to do all the time before they start religiously posting on social media is doing the trial reels method because the trial reels.
[00:24:29 – 00:24:31] Is anyone familiar with Shot Reels?
[00:24:31 – 00:24:32] What it does.
[00:24:32 – 00:24:33] The use case for it.
[00:24:38 – 00:24:41] Yeah, bro, I I actually did one.
[00:24:41 – 00:24:43] It's just you post reels.
[00:24:43 – 00:24:44] where your followers can't see.
[00:24:45 – 00:24:47] To see how it performs, it performs well you can
[00:24:47 – 00:24:48] put it on your main feed.
[00:24:49 – 00:24:49] Yep.
[00:24:49 – 00:24:50] Exactly.
[00:24:51 – 00:24:51] So
[00:24:51 – 00:24:55] Is there a certain amount you should try at a certain time?
[00:24:55 – 00:25:00] Do you ever like post the same one three times or all different videos? What's your deal with Travis?
[00:25:00 – 00:25:01] Yeah, so
[00:25:02 – 00:25:03] What I just dropped.
[00:25:03 – 00:25:04] End?
[00:25:04 – 00:25:09] What I just dropped in, this is a great thing to talk about while we're on the topic of hooks.
[00:25:09 – 00:25:10] Because
[00:25:10 – 00:25:13] You basically want to change one thing.
[00:25:13 – 00:25:18] one consistent across multiple different videos and then keep everything else the same.
[00:25:18 – 00:25:22] And the only other changes that you make to that video will be based on data.
[00:25:23 – 00:25:25] And I'll explain what that means. So.
[00:25:25 – 00:25:28] If I have a video where I'm talking about
[00:25:28 – 00:25:29] How
[00:25:29 – 00:25:35] I made my first hundred thousand dollars a month and how you can too. Okay, whatever the hell the hook is. I come up with three hooks on that topic.
[00:25:36 – 00:25:39] Then the body of the video is the same.
[00:25:39 – 00:25:42] I do the same CTA every time.
[00:25:42 – 00:25:45] And I post it three times onto Trial Reels.
[00:25:46 – 00:25:50] The beautiful thing about these social media platforms is they have really good analytic
[00:25:50 – 00:25:51] tracking.
[00:25:52 – 00:25:52] Okay, so
[00:25:53 – 00:25:59] If I want to go in and see, like, is the CTA landing? Where are we losing the retention of the viewers?
[00:25:59 – 00:26:01] All I would go on and click
[00:26:01 – 00:26:01] You
[00:26:01 – 00:26:02] Honor
[00:26:02 – 00:26:04] On the social media platform, you would click
[00:26:04 – 00:26:07] Check analytics or the analytic page.
[00:26:07 – 00:26:08] I'm sure you guys
[00:26:08 – 00:26:11] Have done that before. I've like checked your analytics as long as you're on a business account.
[00:26:11 – 00:26:12] Um
[00:26:13 – 00:26:15] And it'll show you a retention graph.
[00:26:15 – 00:26:17] I like to use Instagram edits.
[00:26:18 – 00:26:23] Through Instagram and post via Instagram edits. So if you guys don't have that downloaded, you should because they have the best.
[00:26:23 – 00:26:24] Analytic tracking.
[00:26:24 – 00:26:24] Um
[00:26:25 – 00:26:28] for Instagram and then TikTok has it internally.
[00:26:28 – 00:26:28] Bye.
[00:26:29 – 00:26:34] I I take those videos and I look at the retention graph and it'll show you where people drop off.
[00:26:35 – 00:26:37] So the hypothesis that I could come to
[00:26:38 – 00:26:40] Is number one.
[00:26:40 – 00:26:41] What hook?
[00:26:42 – 00:26:42] Worked
[00:26:42 – 00:26:43] The best.
[00:26:44 – 00:26:46] What hook resonates with the audience?
[00:26:46 – 00:26:47] Better.
[00:26:48 – 00:26:50] The second thing I could come to a conclusion on
[00:26:50 – 00:26:51] Is
[00:26:51 – 00:26:58] Where are people dropping off? Are they dropping off at the hook? Are they dropping off at the body of the video? Are they dropping off at the very end?
[00:27:00 – 00:27:00] And
[00:27:00 – 00:27:01] If I
[00:27:02 – 00:27:07] Typically what you'll see, especially if you're changing the hook, which is the primary thing I would change in the beginning.
[00:27:07 – 00:27:10] You will see which hook lands the best.
[00:27:11 – 00:27:19] And if it really lands and you have like a super high retention and then it drops off all of a sudden, it's like maybe your CTA was weird or maybe the body of the video just wasn't that entertaining.
[00:27:20 – 00:27:24] But one of those is gonna have a standout hook retention.
[00:27:24 – 00:27:29] That's your winner, re-replicate that the similar hooks to that with different topics.
[00:27:29 – 00:27:30] or ideas.
[00:27:30 – 00:27:31] Does that make sense?
[00:27:32 – 00:27:33] And then usually you can post like three to five.
[00:27:38 – 00:27:43] But yeah, are you guys following me there on the on like how to track the data and try different hooks?
[00:27:44 – 00:27:45] Yeah.
[00:27:47 – 00:27:49] Yo, Rick, could you grab me that uh door dash?
[00:27:50 – 00:27:51] Yeah, my friggin'.
[00:27:51 – 00:27:52] Terrible chicken.
[00:27:53 – 00:27:54] That Asian restaurant.
[00:27:55 – 00:27:55] Yeah.
[00:27:56 – 00:28:00] No, I didn't eat any of it. Dude, it's absolutely disgusting. Worst thing I've ever had. Actually, dude, I
[00:28:00 – 00:28:06] You know, I think about content ideas all the time. I I would love to make a video about how bad that chicken was.
[00:28:08 – 00:28:09] Straight up.
[00:28:10 – 00:28:10] There's
[00:28:10 – 00:28:13] Terrible. Ruin like life ruining.
[00:28:13 – 00:28:14] Okay, so.
[00:28:15 – 00:28:23] Next thing we're gonna move on to. So we have visual hooks, text hooks, verbal hooks. I'm gonna be sending out a bunch of different resources for you guys.
[00:28:24 – 00:28:28] or like coming up with the ideation process of those hooks.
[00:28:28 – 00:28:32] We've been working on a lot of our SOPs and resources pretty heavily.
[00:28:32 – 00:28:38] As of late, just to make sure that they're up to date and that we get a clear path forward for everybody that's coming in in the sense of.
[00:28:39 – 00:28:40] What to do.
[00:28:41 – 00:28:41] When to do it.
[00:28:42 – 00:28:42] How to do it.
[00:28:43 – 00:28:43] 'Kay.
[00:28:44 – 00:28:44] Now
[00:28:45 – 00:28:56] Um from this point, I'm gonna open it up to QAs. And if we don't do QAs, then we're just gonna go rate different hooks from different creators that I really like, and I'll do reviews and explain why the video worked or why it didn't work.
[00:28:58 – 00:29:00] It looks like Marcos is literally closing a deal right now.
[00:29:04 – 00:29:06] I bet you he is.
[00:29:10 – 00:29:11] I actually think he is.
[00:29:11 – 00:29:12] Okay, so.
[00:29:12 – 00:29:13] Um
[00:29:13 – 00:29:14] If nobody has any questions.
[00:29:15 – 00:29:22] Then, what we're gonna do next is I'm gonna pop open this one. So, I was doing some deep diving into a couple of different Instagram accounts that I really liked.
[00:29:22 – 00:29:23] From salespeople.
[00:29:23 – 00:29:27] They're in the sales world. Let me pull up our document on this really quick.
[00:29:28 – 00:29:29] See you work.
[00:29:29 – 00:29:30] Count uh
[00:29:33 – 00:29:34] Um
[00:29:35 – 00:29:37] Alright, I'm pulling up the link right now.
[00:29:39 – 00:29:40] Oh.
[00:29:40 – 00:29:41] Where is he?
[00:29:43 – 00:29:43] Bye bye.
[00:29:44 – 00:29:44] Jackson Bubba.
[00:29:46 – 00:29:48] Have you guys seen this guy before? His name is Jackson Bubba.
[00:29:51 – 00:29:55] Mop hop, man, make a friend help a friend.
[00:29:55 – 00:29:56] Ha ha ha.
[00:29:56 – 00:29:58] He's good, dude. He's really good.
[00:29:58 – 00:29:59] Um
[00:30:00 – 00:30:04] Okay, let me let me share my screen really quick. This guy has blown up.
[00:30:05 – 00:30:07] And he blew up fast.
[00:30:07 – 00:30:08] I remember texting him when he was out like
[00:30:09 – 00:30:13] I don't know, he's probably like twenty K and I'm just like, dude, you're about to blow up. Like, you're doing it right.
[00:30:13 – 00:30:15] I could tell right off the bat,'cause again
[00:30:15 – 00:30:18] The hooks were good, and he just had an eye for content.
[00:30:18 – 00:30:19] But if we move over.
[00:30:20 – 00:30:22] This is actually a reference that I used.
[00:30:22 – 00:30:26] on the video today about making sales videos.
[00:30:26 – 00:30:28] Definitely not the type that I was making.
[00:30:28 – 00:30:29] Um
[00:30:29 – 00:30:32] But it was one of the versions that you can make.
[00:30:32 – 00:30:37] What I want to do is, I'm just gonna watch the first like five seconds of this video, and I want you guys to point out.
[00:30:39 – 00:30:40] What about the hook?
[00:30:40 – 00:30:43] Worked like because this is a very different style of doing a hook.
[00:30:44 – 00:30:46] still falls under the four categories, it always does, but like this is
[00:30:47 – 00:30:48] I just want you guys to watch.
[00:30:50 – 00:30:51] And let me see here.
[00:30:51 – 00:30:57] That is the shittiest fucking job I've ever had anybody do.
[00:30:59 – 00:31:01] Can anyone tell me why that worked?
[00:31:01 – 00:31:02] and what type of hook it was.
[00:31:09 – 00:31:10] You guys were able to hear that, right?
[00:31:11 – 00:31:19] Yeah, no, I mean it's a verbal hook, but it's hella abrasive, so it just catches you off guard. Shock factor. Shock factor, exactly, is insane.
[00:31:19 – 00:31:22] It was a lady, it was a customer, that was extremely pissed off.
[00:31:22 – 00:31:24] saying something absolutely insane.
[00:31:25 – 00:31:27] So what we call that.
[00:31:28 – 00:31:29] is a teaser.
[00:31:30 – 00:31:31] Alright, teasers.
[00:31:31 – 00:31:34] work really really well and I explained this when I when creating
[00:31:35 – 00:31:37] content for sales videos. But
[00:31:38 – 00:31:39] Let's say that you have
[00:31:39 – 00:31:43] a video that's extremely value dense or value packed or
[00:31:44 – 00:31:45] has like a
[00:31:46 – 00:31:50] A payoff at the end or something crazy that happens.
[00:31:51 – 00:31:53] But like the beginning of the video,
[00:31:53 – 00:31:54] It's just kind of like
[00:31:55 – 00:31:55] Boring.
[00:31:57 – 00:31:57] Right.
[00:31:58 – 00:32:01] It's just a little bit boring. Like he started off the video saying, all right, guys.
[00:32:02 – 00:32:03] So there's this sales
[00:32:03 – 00:32:06] Tactic, okay? That is not a good hook.
[00:32:07 – 00:32:09] Alright guys, here's the sales tactic.
[00:32:10 – 00:32:11] And it's like
[00:32:12 – 00:32:16] There's a lot of ways that he could have came up with the hook framework that may have worked here.
[00:32:16 – 00:32:18] But instead he did what it
[00:32:18 – 00:32:19] What's called a teaser.
[00:32:20 – 00:32:21] He pulled.
[00:32:21 – 00:32:24] The most value-packed or entertaining part of the video
[00:32:26 – 00:32:29] Cut it out, slapped it in the first two seconds.
[00:32:29 – 00:32:31] to foreshadow
[00:32:31 – 00:32:33] What was going to happen in the video?
[00:32:34 – 00:32:36] Okay, it was it was
[00:32:36 – 00:32:41] Again, it stopped the scroll because it was something that incited an emotion. It's like, holy shit, that lady's going crazy.
[00:32:41 – 00:32:41] 'Kay.
[00:32:41 – 00:32:43] Very shock factor, so it stopped to scroll.
[00:32:44 – 00:32:45] And
[00:32:45 – 00:32:52] It promised some type of payoff, and that payoff was entertainment later, understanding how the hell that woman got so hot.
[00:32:53 – 00:32:53] Right.
[00:32:54 – 00:32:57] And I know that within the first two seconds, like genuinely think about it.
[00:32:57 – 00:32:59] If you land on this video,
[00:32:59 – 00:33:00] Subconsciously
[00:33:00 – 00:33:03] What do you already know is going to happen?
[00:33:05 – 00:33:08] Like this video is gonna be about how that lady got to that point where she was so freaking hot.
[00:33:09 – 00:33:11] Like she's going crazy. And then.
[00:33:11 – 00:33:17] He goes into reinforcing, you know, this is a sales tactic that I'm going to teach you guys today, but I want to stay on it. Why?
[00:33:18 – 00:33:21] Because there was so much shock factor emotion evoked.
[00:33:21 – 00:33:28] From the lady, and it really got me curious. I have a lot of curiosity, and I know that he's gonna show how she got there in that video.
[00:33:28 – 00:33:28] So
[00:33:29 – 00:33:31] Using that little trailer hook.
[00:33:31 – 00:33:33] In the beginning, it's still a verbal hook, but it's like
[00:33:33 – 00:33:35] I don't know, maybe we could call it a trailer hook.
[00:33:35 – 00:33:36] I've never seen it.
[00:33:37 – 00:33:38] Seeing people like teach about it before.
[00:33:39 – 00:33:41] But beautiful things. I'll show you again one more time.
[00:33:41 – 00:33:49] That is the machiniest fucking job I've ever had anybody do. Alright, guys, this is still training I learned about the piss boat. So I've got this customer.
[00:33:50 – 00:33:51] I also like how
[00:33:51 – 00:33:54] Right after he does that, he calls it the piss boat.
[00:33:54 – 00:33:57] He's literally just teaching people how to level with the customer.
[00:33:58 – 00:34:03] Like that's it's literally all he's really doing is just teaching them how to level as a customer that's really pissed off, like take their side.
[00:34:03 – 00:34:04] There's like
[00:34:05 – 00:34:07] You know, the the concept that he talked about was like taking
[00:34:08 – 00:34:16] They're really mad, and then you get on their team and get really mad at the company that you work for with them, type of thing. It's like leveling and taking their side.
[00:34:16 – 00:34:16] Um
[00:34:17 – 00:34:19] And he used like a cool word for it called the piss boat.
[00:34:19 – 00:34:20] 'Kay.
[00:34:20 – 00:34:20] Again.
[00:34:21 – 00:34:23] Building curiosity, you don't really know what it is.
[00:34:24 – 00:34:25] You want to stay on the video to figure it out.
[00:34:27 – 00:34:30] That is the concept: is how do I stop the scroll?
[00:34:30 – 00:34:33] How do I build a curiosity, evoke an emotion?
[00:34:33 – 00:34:36] and make them stay for some type of payoff.
[00:34:37 – 00:34:38] Mm-hmm.
[00:34:38 – 00:34:40] So if you guys have had any sales calls, I mean
[00:34:41 – 00:34:44] All of you guys are in sales. What is the craziest
[00:34:45 – 00:34:48] thing that somebody has said to you on a sales call.
[00:34:49 – 00:34:52] We'll make this a little interactive, seeing as how we have a very quiet room today. Everyone's depressed.
[00:34:54 – 00:34:59] What is the craziest thing someone has said to you on a sales call or in a sales encounter?
[00:34:59 – 00:35:01] Other than getting a gun pulled on you, that doesn't count.
[00:35:02 – 00:35:03] We turn it over, guys.
[00:35:04 – 00:35:05] I'll tell you mine.
[00:35:05 – 00:35:08] I was uh I was actually out in Kentucky with you, dude.
[00:35:08 – 00:35:10] And I had a lady literally
[00:35:11 – 00:35:11] Tell me
[00:35:12 – 00:35:15] Wh when we were when I got her all signed up and everything, she looks at me and she goes,
[00:35:16 – 00:35:20] Well there's not there's not gonna be any colored folk working on the property, is there?
[00:35:20 – 00:35:21] Oh he
[00:35:21 – 00:35:22] Well
[00:35:24 – 00:35:26] And I can literally put at the beginning is like
[00:35:28 – 00:35:32] Watch this, watch this, okay guys? I'm gonna take that and I'm gonna give you the idea right now, okay?
[00:35:33 – 00:35:42] That is the shittiest fucking job I've ever had. So I'm selfie videoing on the doors because you can't you'd have to selfie video on the doors. You just kind of like hide your phone and prop it up a little bit.
[00:35:42 – 00:35:45] And I would put racist client incoming.
[00:35:49 – 00:35:51] See how that directly translates?
[00:35:53 – 00:35:57] Like how that same exact encounter could directly translate. I just changed.
[00:35:57 – 00:35:58] The title a little bit.
[00:36:00 – 00:36:03] It'd be the same crazy thing that she said in the first couple of seconds.
[00:36:04 – 00:36:07] And then I'd go into the beginning of the encounter.
[00:36:07 – 00:36:09] Or I do a little breakdown, like, all right, guys.
[00:36:10 – 00:36:12] I do door-to-door sales in Kentucky.
[00:36:13 – 00:36:18] Obviously, there is a freaking race of people down here, and I found the worst of them all today, and she still signed up.
[00:36:19 – 00:36:21] or something along those lines, right?
[00:36:21 – 00:36:35] Now they're like, no way. Okay, let me watch. Let me check it out. Let me stay on the video. It has the stop the scroll effect. It's very shock factor. And then I reinforce that they're going to get what they came for, what hooked them in that first couple of seconds.
[00:36:36 – 00:36:36] Right.
[00:36:38 – 00:36:39] Does that make sense?
[00:36:43 – 00:36:48] This is the easiest one to do for sales calls, because sales calls, it's really hard to come up with good hooks.
[00:36:48 – 00:36:49] When like
[00:36:50 – 00:36:53] You're literally like you start off the sales call like, hey, how's it going?
[00:36:54 – 00:36:56] Sorry, that's not the best hook in the world.
[00:36:58 – 00:37:00] I made another one today I showed.
[00:37:01 – 00:37:03] me doing the option close.
[00:37:05 – 00:37:09] So I I showed like the beginning of the video is like, yeah, so do you want to do the
[00:37:09 – 00:37:09] Um
[00:37:10 – 00:37:13] Do you just want to pay the five thousand a month or do you want to do the ten thousand and get the third month for free?
[00:37:15 – 00:37:21] Okay, that was like the hook to the video. It wasn't as great as this one right here, but it was as good as I could get out of the sales call.
[00:37:22 – 00:37:24] And then I think the text on it was like,
[00:37:24 – 00:37:25] P O V
[00:37:25 – 00:37:28] or like the 10-step framework to close 100K a month.
[00:37:28 – 00:37:29] or something like that.
[00:37:31 – 00:37:32] Something pretty simple.
[00:37:32 – 00:37:32] Alright.
[00:37:33 – 00:37:33] Um
[00:37:35 – 00:37:37] I mean that's pretty much it. That's all I got for you guys.
[00:37:38 – 00:37:39] You literally put 80%.
[00:37:40 – 00:37:41] of your time into the first
[00:37:42 – 00:37:43] Who's Ryan Hocker?
[00:37:43 – 00:37:43] Um
[00:37:44 – 00:37:46] You already put eighty percent of your time into the first
[00:37:47 – 00:37:48] Fight.
[00:37:48 – 00:37:50] Two to five seconds.
[00:37:50 – 00:37:51] Two to four seconds really.
[00:37:52 – 00:37:53] And
[00:37:53 – 00:37:56] the rest will be taken care of. And then I sent out the trial reels method.
[00:37:56 – 00:37:57] That way you can try.
[00:37:58 – 00:37:58] Different
[00:37:59 – 00:37:59] Books.
[00:38:00 – 00:38:01] On the same video.
[00:38:02 – 00:38:05] Test different hooks, see which ones work, check the data in the back end.
[00:38:05 – 00:38:07] I'm using the trial reels method.
[00:38:07 – 00:38:08] And then finally.
[00:38:08 – 00:38:09] Um
[00:38:11 – 00:38:15] Gosh, I I literally lost my frame of thought. Uh yeah, no, you just do the trial rules method.
[00:38:15 – 00:38:16] Oh yeah, and then ads.
[00:38:16 – 00:38:17] Um
[00:38:18 – 00:38:23] Ads are a little bit different. Remember ads are a little bit different. Speak to your direct ICP and then speak to their pain point.
[00:38:27 – 00:38:29] Any questions?
[00:38:30 – 00:38:32] Visual verbal caption title.
[00:38:35 – 00:38:36] Can I have a quick point?
[00:38:37 – 00:38:37] Yeah, go ahead.
[00:38:38 – 00:38:40] So on one of your videos
[00:38:40 – 00:38:43] Well, multiple of your videos, I see like the, at the bottom, like DM me this.
[00:38:44 – 00:38:47] for this do you though in every single video or if it's like a different style video like
[00:38:49 – 00:38:51] Do you mean in the caption?
[00:38:51 – 00:38:52] Yeah.
[00:38:52 – 00:38:55] Like like the actual caption, like the text.
[00:38:55 – 00:38:56] Section.
[00:38:56 – 00:38:56] Yeah.
[00:38:57 – 00:38:57] Yeah.
[00:38:58 – 00:39:05] I don't, I wouldn't do that on every video. There's periods where I've tried it on all videos, like when I was originally getting my crazy lead flow.
[00:39:06 – 00:39:07] And
[00:39:07 – 00:39:08] You don't want to do it
[00:39:08 – 00:39:12] too much, but I also didn't run like a content strategy.
[00:39:13 – 00:39:24] I didn't run a s a content strategy where I'd post like different styles of content. If you've ever watched the videos on like the three pillars of content before, like some videos, it absolutely makes no sense whatsoever.
[00:39:25 – 00:39:28] Where some videos it is more niche specific.
[00:39:28 – 00:39:28] Right.
[00:39:29 – 00:39:34] There's like if I have a viral video, for example, my plan A, plan B video, plan A, get a wife.
[00:39:34 – 00:39:35] Raise a family.
