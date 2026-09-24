# 020-Strategic Pattern Recognition (March 18, 2026)

- **Title:** 020-Strategic Pattern Recognition (March 18, 2026)
- **Source filename:** 020-Strategic Pattern Recognition (March 18, 2026).mp4
- **Duration:** 1:05:27
- **STT engine:** onnx-asr / NVIDIA Parakeet TDT 0.6B v2 (int8) + Silero VAD
- **Date:** 2026-08-25

## Transcript

[00:00:00 – 00:00:00] So
[00:00:01 – 00:00:04] Today's call is on a few things, right? It's on pattern recognition.
[00:00:04 – 00:00:07] It's on figuring out what your baseline is.
[00:00:08 – 00:00:10] Feedback loops. How do I get feedback?
[00:00:11 – 00:00:17] And understand where I'm going, right? Like, how do I predict what's happening based on my current feedback loops?
[00:00:17 – 00:00:22] How do I predict behavior early and correct it before it costs me a lot?
[00:00:22 – 00:00:22] Now
[00:00:23 – 00:00:25] Why do I want to teach this to you guys today? I'll tell you.
[00:00:27 – 00:00:29] My AI, I don't know how much you guys know about it.
[00:00:29 – 00:00:30] So
[00:00:30 – 00:00:32] I'm going to give you guys a quick story. Just happened recently.
[00:00:33 – 00:00:36] I had a client who came to hypnosis certification.
[00:00:36 – 00:00:44] At the hypnosis, he pitches me, right? Because we had this come, I had this idea come out over a year ago, and I launched a program called Apex.
[00:00:44 – 00:00:47] Actually, exactly a year ago, in like one week, I launched that program.
[00:00:48 – 00:00:56] And the idea was: I was like, ah, how hard can it be to get a hypnosis AI going? I told Jack, just get this going. This will be innovative, this will be amazing.
[00:00:56 – 00:00:58] We'll launch it on a program called Apex.
[00:00:59 – 00:01:04] And the technology just wasn't there at the time. There was nothing we could do. Now, he's been following me for quite some time.
[00:01:05 – 00:01:06] And he knew that we attempted that.
[00:01:07 – 00:01:09] And he came up to me at the hypnosis certification last year.
[00:01:10 – 00:01:11] Uh in the summer.
[00:01:11 – 00:01:12] And
[00:01:12 – 00:01:13] He goes
[00:01:15 – 00:01:16] I can help you do it.
[00:01:17 – 00:01:18] I'm like, okay.
[00:01:19 – 00:01:20] So I told him, I'm like, look.
[00:01:21 – 00:01:24] You know, in exchange for you doing it, because you wanted to do it for free. Literally, he was like, I'll do it for you for free. No problem.
[00:01:25 – 00:01:33] I'm like, let me give you access to breakthrough accelerator for 50K for the year, right? And he's like, oh my God, that's amazing. I'll do it. So he came to my house.
[00:01:33 – 00:01:34] And for two weeks straight.
[00:01:35 – 00:01:53] He's working on this AI, and I'm giving him feedback. I'm telling him, here's what has to change with the hypnosis. Here's how you have to improve it. You got to make sure the induction sounds like this. This is fucking up here, right? These words don't make sense. Like, he's like, okay, got it. All right. And I give him, I pretty much designed the whole thing. I sat with him and he did the code stuff. He used AI to do the code. I don't know how to do any of that.
[00:01:53 – 00:02:06] But it wasn't anything that impressive. I saw him plugging it into Claude and Claude code. And he wasn't really using his own knowledge. He was just typing in some prompts and he'd copy and paste the code. And he understood it more than me because he went to MIT or something.
[00:02:06 – 00:02:07] Anyways.
[00:02:08 – 00:02:18] Then he goes, we launch it. He waits for us to launch it. I told Jack, I'm like, Jack, please make sure you own this source code and everything. He's like, no worries. So Jack gets on meetings with him, but I didn't realize that.
[00:02:18 – 00:02:20] Jack didn't get the ownership.
[00:02:21 – 00:02:26] And I told Jack, I'm like, by the way, you got the ownership for everything. He goes, no, the guy keeps beating around the bush.
[00:02:26 – 00:02:31] I go, okay. So I keep texting guys, hey man, I need I need you to transfer ownership.
[00:02:31 – 00:02:39] Today, like because I see that it's fishy, like the fact that he hasn't done it yet is weird, right? So, I'm talking to him and he sends me an audio, and the audio is.
[00:02:40 – 00:02:42] Hey, uh, hey, buddy, uh, I don't appreciate you.
[00:02:43 – 00:02:44] asking for ownership.
[00:02:44 – 00:02:46] As as of right now.
[00:02:46 – 00:02:48] I own the anth, not you.
[00:02:48 – 00:02:50] Uh and
[00:02:50 – 00:02:57] You know, I don't appreciate that. And, you know, I'm considering like, you know, on the low end, I would accept 30 to 40% equity in it.
[00:02:58 – 00:03:08] And I'm like, okay, cool. We'll chat soon. I have seminars this week. No worries. Instantly, I saw the pattern, right? Pattern, I knew, I knew by him not giving us ownership, I was already needing to do it. So, what did I do?
[00:03:08 – 00:03:12] I had already started developing my own version.
[00:03:12 – 00:03:13] Would Jack separately?
[00:03:14 – 00:03:18] So we buy time, we buy time, we keep buying time.
[00:03:18 – 00:03:19] And then what ends up happening?
[00:03:20 – 00:03:21] Uh
[00:03:21 – 00:03:38] I end up launching version two, which he has zero control over because he didn't write any code. He doesn't own my voice. He doesn't own my hypnosis. He doesn't own anything else. All he owned was whatever he wrote, right? Theoretically, he doesn't even own that, but theoretically, that's all he owned, right? So, long story short, because I was able to predict it, here's what
[00:03:37 – 00:03:42] Here's what this motherfucker did. We were waiting for the right time to transfer everyone over because of the pain in the ass.
[00:03:42 – 00:03:44] Um and we wanted to get everything perfect.
[00:03:44 – 00:03:54] Three days before everyone's subscription is renewed, he pulls the plug without telling anyone because he's just an asshole. Right. And I'm like, okay, all good. We transferred everyone over to the new one.
[00:03:55 – 00:04:02] And it's all fine. Now, the reason that didn't end up costing me hundreds of thousands of dollars, literally, like about a quarter million dollars in renewals.
[00:04:03 – 00:04:14] Was because of the fact that I saw the pattern way ahead of time just off of one voice note that he sent me, right? Now, what I want you guys to realize is there are always patterns. I can predict when someone's going to quit.
[00:04:15 – 00:04:18] Way before they quit. Like, I'll get on Zoom with Jack.
[00:04:19 – 00:04:35] Jack, tell me if I've ever been wrong. No, don't kiss my ass. Honestly, we'll be on Zoom with a sales team. I'll be on Zoom with anyone, any employee. They won't say a word. They'll just have their face on or their camera on or their camera won't be on. And I'll tell Jack, they're about to quit. You need to find a replacement. Like, what are you talking about? They didn't say anything. I'm like, I'm telling you, they're going to quit. They're going to quit in two hours.
[00:04:36 – 00:04:39] Not even an hour and a half goes by. They send a message saying, I quit.
[00:04:39 – 00:04:49] Or they'll do something. I'll be like, hey, that guy's about to steal. You got to get him off this client, like out of the team. Next thing you know, a client ends up: hey, is this guy supposed to sell us on this? And you go, no. What'd you say, Jack?
[00:04:51 – 00:04:56] Every single time, every time that I don't even know what you're looking at.
[00:04:57 – 00:04:57] I
[00:04:57 – 00:04:59] I'm about to teach it. So.
[00:04:59 – 00:05:02] The point is, how do you predict?
[00:05:03 – 00:05:09] What one you're going to be doing. Like right now, I'll give you guys an example of what we're teaching today, okay?
[00:05:10 – 00:05:10] Right now.
[00:05:11 – 00:05:12] I'm eating.
[00:05:13 – 00:05:15] About 180 grams of protein per day.
[00:05:16 – 00:05:20] I'm at about 1700 calories a day on average.
[00:05:20 – 00:05:23] I walk around 7,000 steps, which is not that much.
[00:05:23 – 00:05:27] And I'm doing a pretty heavy workout, lifting five to six times a week.
[00:05:28 – 00:05:29] Where
[00:05:29 – 00:05:35] What trajectory do you think I'm on in terms of where my body's going to be in maybe a month or nothing now?
[00:05:37 – 00:05:41] probably look pretty crazy, right? Probably be in pretty great shape. Now
[00:05:41 – 00:05:42] Why?
[00:05:42 – 00:05:44] Because the pattern
[00:05:44 – 00:05:47] indicates that that's where I'm heading. So
[00:05:47 – 00:05:50] I want you guys to understand that you don't lose.
[00:05:51 – 00:05:54] You generically don't lose because of something that happened today.
[00:05:54 – 00:05:57] You lose because of things that happened.
[00:05:57 – 00:06:00] over time that you fail to notice
[00:06:00 – 00:06:01] And then
[00:06:01 – 00:06:02] It hits you.
[00:06:03 – 00:06:06] The punishment for it. For example,
[00:06:06 – 00:06:06] You know
[00:06:07 – 00:06:11] Someone starts showing up late to meetings and he's your employee.
[00:06:12 – 00:06:12] Then
[00:06:13 – 00:06:17] They talk back or they say yeah, yeah, yeah, but they don't do what they say they're gonna do.
[00:06:17 – 00:06:23] All of a sudden, you realize you're short$100,000 in sales that month because he didn't perform.
[00:06:23 – 00:06:27] Well, you could see the beginning of the month that they stopped performing.
[00:06:27 – 00:06:38] Because they were late. They stopped saying they're going to do what they're going to do. So all of these little things add up. And all of a sudden, now you're short$100,000. Or they start, they say, they complain one time about someone else.
[00:06:39 – 00:06:51] And you're like, huh, this person has a gossiping problem. Next thing you know, one bad apple turns their entire team into bad apples, and everyone has to be fired. You have to start from scratch, right? There's always patterns that begin.
[00:06:51 – 00:07:00] That most people overlook because they didn't cross a certain line or a threshold. Because what you're doing is you're not predicting what that pattern says about what's to come.
[00:07:00 – 00:07:05] Today I want to kind of give you guys that connection. On top of that, I want to show you how your patterns affect.
[00:07:05 – 00:07:13] Your behavior. Now, in order to know what your patterns are, in order to understand what's changed, you have to understand this word, it's called a baseline.
[00:07:14 – 00:07:27] Right. So we have to know the baseline. You have to detect whenever things change early, like what changed in my baseline or other people's baseline. You have to understand where the pattern is going to take this person, including yourself.
[00:07:27 – 00:07:33] You have to intervene very quickly. The faster you do it, the better. And then you have to create feedback loops.
[00:07:33 – 00:07:37] which tell you if you're actually on track or on off track, right? So.
[00:07:37 – 00:07:38] The biggest thing is
[00:07:39 – 00:07:46] You're going to take signals that show up before there are consequences, right? So by the time something is usually bad,
[00:07:47 – 00:07:49] It has already been bad for a while.
[00:07:50 – 00:07:51] in some subtle form.
[00:07:52 – 00:07:56] It didn't just show up in a negative way. It's been bad.
[00:07:56 – 00:08:09] Someone gave you red flags before the consequence happened. Before someone stole from you, betrayed you, sued you, cheated on you, left you, fought with you, destabilized you, attacked you, killed you. They gave you the red flags before they did it.
[00:08:10 – 00:08:15] Right, a murderer doesn't wake up one day and just stab you. There are
[00:08:15 – 00:08:18] many many red flags that happen before the moment he stabs you
[00:08:19 – 00:08:20] That tells you, hey.
[00:08:21 – 00:08:33] This is probably not the person I should be around. So, realizing, you know, when you have a bad relationship or a weak business performance, or you know, you lose discipline for whatever reason, or you're emotionally unstable.
[00:08:33 – 00:08:47] Uh, your standards go to shit, your team is not functioning the way they should, and maybe you're less attracted to your partner, or you know, you don't trust them, your health is bad. These all have some kind of early pattern that appears.
[00:08:47 – 00:08:51] that you can change. Right. Someone doesn't wake up one day and have a heart attack.
[00:08:51 – 00:08:59] Okay, they have a heart attack because for years they've been eating like shit and they've not been taking care of their health and they've not been active. And then they get a heart attack.
[00:09:00 – 00:09:15] Right, or they're overweight and then they get a heart attack. So it's a pattern that most people ignore until the consequence is there. For example, someone smokes cigarettes, right? This is one of the easiest ones to spot. If you're constantly smoking cigarettes, when do people tend to stop smoking cigarettes?
[00:09:16 – 00:09:28] When something changes, suddenly it's harder to breathe, suddenly it hurts to breathe, suddenly they're worried that maybe there's cancer. They see a video about someone having cancer and it scares them, or they go to the doctor and they go, Yeah, do you know that you have lung cancer?
[00:09:29 – 00:09:33] Holy shit. Now I quit smoking. And in some cases, they don't even quit then.
[00:09:34 – 00:09:36] They don't even care at that point, right? So.
[00:09:36 – 00:09:38] Another example of this is
[00:09:38 – 00:09:39] I was in Bahamas.
[00:09:40 – 00:09:41] And
[00:09:41 – 00:09:42] I
[00:09:42 – 00:09:44] I flew out this girl that I liked.
[00:09:44 – 00:09:47] And I ended up dating her. This was like a girl I was wanting to marry at the time.
[00:09:48 – 00:09:48] Um
[00:09:49 – 00:09:51] She brings her dad to the Bahamas.
[00:09:51 – 00:09:53] Now we're eating dinner. Me
[00:09:54 – 00:09:54] Jack.
[00:09:55 – 00:09:55] Hmm
[00:09:56 – 00:09:56] Her dad.
[00:09:57 – 00:10:00] And I'm looking at her dad and he turns red.
[00:10:01 – 00:10:04] And I say what's wrong and he opens his mouth, but he can't say it.
[00:10:04 – 00:10:09] And I look at Jack, I'm like, Jack, you gotta go get a doctor. You gotta go to an ambulance immediately. He's having a stroke.
[00:10:09 – 00:10:17] And I didn't say it out loud. I just told Jack, I'm like, I'm going to keep everyone here and go get an ambulance. These guys are having a stroke. Turns out he had a stroke.
[00:10:18 – 00:10:36] And he still has consequences from the stroke, right? Take him to the hospital. The doctors are like, oh, you know, the nurses are like, hey, get in the waiting room. I'm like, he just had a fucking stroke. I walk in the back of the room. I didn't give a shit. Like, security comes trying to stop me. I'm like, move. I find the doctor. I'm like, doctor, you know, there's a guy here who just had a stroke. And the doctors are telling me to wait. He's like, they're fucking retarded.
[00:10:36 – 00:10:43] That's what the doctor said. He came out and he watched me immediately, right? Because you're supposed to pull someone. That's like a number one emergency, right? Anyways.
[00:10:44 – 00:10:46] He I saw him a couple years later.
[00:10:46 – 00:10:51] still smokes still drinks still has bad habits still gains weight smokes probably two pack cigarettes a day
[00:10:52 – 00:10:52] Right.
[00:10:52 – 00:11:10] And you look at this, and it's like sometimes people's patterns just have more power over them than anything else. They just can't control it. And this is not where you want to be. So you want to understand where your baseline is, and where is your baseline taking you up until now? Up until now, your current life, your body, your weight, your money, your income, your relationships, all of it.
[00:11:10 – 00:11:13] is the result of things you've already been doing until now.
[00:11:14 – 00:11:27] Now, if you're going to change your baseline, the question is: where does it take you? Does it take you to a place that makes you do better, or does it take you to a place that's making you do worse? Or does it continue taking you on the path you're on now? And the question is: do you like the path you're on now?
[00:11:28 – 00:11:34] Right. So, this is where we're understanding our baseline comes from. So, let's talk about cash flow. Right? Cash flow is obviously important for everyone. Right.
[00:11:35 – 00:11:44] I want you to detect your baseline because whenever your baseline drifts, you can detect some kind of danger. So there's no way you could understand when you're drifting away.
[00:11:44 – 00:12:01] From baseline, if you don't even know what normal looks like, what does my normal day-to-day look like? What does my normal income look like? What does my normal metrics look like? Right in my business, what does normal sales look like? What does normal lead flow look like? What is my show up rate if I have calls booked right on the calendar? What about my team's energy?
[00:12:01 – 00:12:04] What about response time? What does normal look like?
[00:12:05 – 00:12:14] Before I know what the baseline is, right? In relationships, is there an attitude someone has out of nowhere? Why is there an attitude? Is it something I said?
[00:12:14 – 00:12:17] When did it start?
[00:12:17 – 00:12:30] When did it start? That is a very, very, very, very, very, very big one. When did someone change their baseline? So I quickly want to give you guys a mental graph that I use that gives me a lot of clarity on this stuff. Whoops.
[00:12:31 – 00:12:32] Here we go.
[00:12:33 – 00:12:35] So this is your baseline behavior.
[00:12:36 – 00:12:38] You wake up, you're calm, your friends, whatever.
[00:12:39 – 00:12:41] So you got this line. This line is your baseline.
[00:12:42 – 00:12:43] Now.
[00:12:43 – 00:12:53] Let's just say you're in a relationship. Okay. I'll give you my example so you guys can all predict it. So from my perspective, all right, up here is a positive shift. Up here is a negative shift.
[00:12:54 – 00:12:57] Suddenly, you know, you're I'm in a relationship with a girl.
[00:12:58 – 00:12:59] No
[00:12:59 – 00:13:03] And she went out with her friends last night for dinner.
[00:13:04 – 00:13:07] And got back home late. I was asleep. She got home at like three.
[00:13:07 – 00:13:08] And whatever, wake up.
[00:13:09 – 00:13:11] Suddenly, she decides she's going to make the bet.
[00:13:12 – 00:13:15] And she's gonna make me breakfast.
[00:13:15 – 00:13:18] And she's going to be extra loving today.
[00:13:19 – 00:13:22] Is that a deviation from baseline? Yes. When did it start? It started.
[00:13:23 – 00:13:24] This morning.
[00:13:24 – 00:13:35] Now, what happened last night? Last night, she went out with friends, which is probably not necessarily the best thing, but whatever. She went out with friends. So the next morning, there's been a deviation here.
[00:13:35 – 00:13:38] Question is why? Now that's the question.
[00:13:38 – 00:13:39] Why?
[00:13:39 – 00:13:42] Did she talk to her friends about me and fall deeper in love?
[00:13:43 – 00:13:46] You know, is it coming from a place of guilt?
[00:13:47 – 00:13:53] Is it coming from a place of just I missed him? Where is it coming from? We don't know why, but we do know.
[00:13:54 – 00:13:55] There's a deviation.
[00:13:56 – 00:13:58] So now with this deviation, what can we do?
[00:13:59 – 00:14:03] We can use that deviation to figure out what caused the deviation.
[00:14:03 – 00:14:09] Problem is, if I just go, wow, she's so nice today, and I don't think about anything prior, I don't think about this baseline.
[00:14:09 – 00:14:11] I have no idea that anything's even changed.
[00:14:12 – 00:14:16] Then I end up dropping my knee. You know, I end up saying, okay, this is going to be my wife.
[00:14:17 – 00:14:19] I love her. Suddenly she tells me she's pregnant.
[00:14:20 – 00:14:21] Turns out it's not even mine.
[00:14:21 – 00:14:23] Right, as an example.
[00:14:23 – 00:14:27] giving you worst case scenarios, but you have to understand.
[00:14:27 – 00:14:29] Everyone gives you a base lunch.
[00:14:30 – 00:14:35] Why the baseline changes is always important. Now, inversely, same thing, same scenario.
[00:14:35 – 00:14:38] Except instead of her making my bed and making me breakfast.
[00:14:38 – 00:14:39] She has a bad attitude the next day.
[00:14:40 – 00:14:41] Why she got a bad attitude?
[00:14:42 – 00:14:45] Who knows? Could be the same why, but a different strategy.
[00:14:45 – 00:14:57] Maybe now she just wants to break up with me and find a way out. All right. It could be she's trying to figure out, trying to justify her behavior. Who knows? Maybe she didn't do anything. Maybe she's just upset I didn't stay up with her. Maybe she's upset and go out with her. Who knows what?
[00:14:58 – 00:15:00] I don't know why. I do know though that there's been a change.
[00:15:01 – 00:15:14] And my job is to find out what the change was and where this is heading. Her making breakfast for me every day, her making my bed for me every day on the surface that looks like it's headed in a good direction, but the intention.
[00:15:15 – 00:15:34] Is why I need to understand the behavior. Why is she suddenly nicer? Is she more committed to me? Why is she more committed? Does she, what changed here? Right? Is it a fear of loss? Is it genuine appreciation? Is it genuine desire? What is it? Right? If it's random, you guys hang out every day and suddenly she just decides she's going to step it up. Cool.
[00:15:34 – 00:15:51] But maybe she overheard a conversation you had with your best friend talking about how your wife is going to be the one who makes your bed and makes you breakfast every morning, right? Maybe she overheard that. Who knows? The point is, there's been a deviation. The question is: why is there a deviation? Now, when you figure out why, if it's because she got with someone the night before, then you understand that the pattern here is quite bad.
[00:15:51 – 00:16:10] And where things are gonna go, they're only gonna get worse. Even if you forgave it, it will eventually be pretty horrible in a relationship long term. So it's probably not a good person to be with, especially because that's a massive, massive, massive betrayal of trust. And also, how does it affect your behavior? How is it gonna affect your patterns? What are you gonna do differently now, right? So now the question goes: all right.
[00:16:10 – 00:16:11] What do we
[00:16:11 – 00:16:23] You know what do we do from here? Well, this is the point. I want you guys to understand that in every scenario, there is always a baseline. Question is: what's within someone's baseline? For example, if a girl's about to get her period.
[00:16:24 – 00:16:27] Is she going to be as friendly? Could be.
[00:16:27 – 00:16:37] Could be she's more emotional. I had a friend, he's dating a girl. She's crazy before the period. She's perfect. And right before the period, she tries to end the relationship every time. She just loses her fucking mind, right?
[00:16:37 – 00:16:48] So some girls have crazy hormones. Who knows? Some guys, right? If a guy suddenly gets stressed out out of nowhere, you ask him what's going on, you tell him, hey, business has been slow. And you're coming up a week before the first of the month.
[00:16:48 – 00:16:49] It makes sense.
[00:16:50 – 00:16:51] Holy shit, okay, stressed out.
[00:16:52 – 00:16:56] So everyone has a reason for why they're off, but
[00:16:56 – 00:17:01] There has to be a baseline. What is the baseline for where I'm at and why I'm off?
[00:17:02 – 00:17:04] Then you can predict the behavior. Now,
[00:17:05 – 00:17:06] In your body.
[00:17:06 – 00:17:08] There's normal hunger. I'm hungry.
[00:17:09 – 00:17:14] I'm hungry at the same time. Every morning, I have this fucking barbell protein bar and I drink one of these.
[00:17:14 – 00:17:20] That's a normal routine I have every morning. If I woke up today and I am starving.
[00:17:20 – 00:17:22] Way different than normal.
[00:17:23 – 00:17:25] I have to ask why am I suddenly hungrier today?
[00:17:26 – 00:17:29] Is it because I'm hitting a different body fat?
[00:17:29 – 00:17:39] Is it because I played basketball suddenly for the first time and did zone three cardio and my heart was at 160 for an hour? Is that why? Probably why, right? There's always a reason, or vice versa.
[00:17:39 – 00:17:42] I start getting extra tired. Why am I so tired today?
[00:17:42 – 00:17:55] I slept 12 hours. Why am I so tired? Is it because I'm low on carbs and my glycogen levels low? Is it because I'm dehydrated? No, it can't be that because I've been consistent. Then maybe I'm getting sick. Maybe I'm low on vitamin D. Let's take vitamin D.
[00:17:56 – 00:18:01] No matter what, I'll take some vitamin D anyways, and then maybe I should get the sauna and a rest today because I must be getting sick.
[00:18:02 – 00:18:09] Well, everyone else suddenly around me is sick. Turns out they were getting sick. I predicted it beforehand. I didn't push myself, I didn't get sick.
[00:18:10 – 00:18:29] Right. So, this is becoming aware of patterns within your body, right? Inflammation, right? How much output? How much sleep? Is it consistent? Right? In my mind, am I focusing normally? Am I as confident as normal? Am I as decisive? Or am I emotionally unstable for some reason? What's going on with me internally? So you got to figure out what your baseline is, right?
[00:18:30 – 00:18:36] If your baseline is undefined, which is most people, they don't know what their baseline is, maybe they do at some intuitive level, right?
[00:18:36 – 00:18:39] But if you're not aware of your actual baseline.
[00:18:40 – 00:18:43] you become vulnerable to what I call rationalization.
[00:18:44 – 00:18:50] For your new baseline. So I don't know if you ever seen someone be in a bad attitude. They're like, you know, I'll call it out. I'm like, what's your problem?
[00:18:51 – 00:18:51] There you go.
[00:18:52 – 00:18:56] I have no problem. Everything's normal today. No, it's not normal. Something's obviously off.
[00:18:56 – 00:18:57] But they can't
[00:18:57 – 00:19:08] They can't understand it because they don't know what their baseline is. And someone who lacks identity, someone who doesn't know who they are, someone who has a hard time getting in a routine or being consistent, who has a lack of purpose.
[00:19:09 – 00:19:27] They have a hard time identifying what normal looks like because normal is always changing. Normal is changing when they're with one guy, normal is changing with a different friend group, normal is changing when they're around. So they don't really know what their baseline is. And this is the person who's the most volatile to shifting, right? They're always drifting. They have, it's called an identity drift. They're drifting from one identity to the next.
[00:19:27 – 00:19:47] They don't know who they are. Now, like on the last call, the biggest problem people have is that they're attached to an old identity. And that old identity, right, has a lot of contradictions. So, really understanding where your baseline has been gives you extreme, extraordinary awareness on where your life is going. I had to get very good at predicting this for multiple reasons. One,
[00:19:47 – 00:19:52] If I was off and I had all this responsibility early on, then I knew that.
[00:19:52 – 00:19:53] I would fail.
[00:19:53 – 00:20:07] So I noticed whenever I was off, I'd make less money and people who counted on me would be let down. So I could not be off. I had to learn how to be consistent. I had to learn how to get into a state that I was consistently taken care of. I had to predict other people around me because I knew that if I let people in,
[00:20:08 – 00:20:19] That it could destabilize me. So I had to learn how to predict other people's behavior. I had to learn how to not trust people in my company who might let me down or betray me or fuck me over, right? I had to learn how to predict that.
[00:20:20 – 00:20:23] You know, a big part of this is if you have an undefined baseline.
[00:20:23 – 00:20:38] Your brain will go, it's probably nothing. I'm probably overthinking, it's just temporary. But if you ignore the red flag, again, the consequences are around the corner. So it's understanding what they are, right? Now, realize this: this is a core principle of today's lesson.
[00:20:38 – 00:20:41] Every pattern has the trajectory.
[00:20:41 – 00:20:50] Every single one, everything you do has a trajectory, right? If I go to the gym every day, I'm on a diet, what's the trajectory? I'm going to be in great shape, I'm going to lose weight, I'm going to look great, right? That's the trajectory.
[00:20:50 – 00:20:51] If I
[00:20:51 – 00:20:54] am eating like a pig every day.
[00:20:54 – 00:20:55] I'm going to get fat.
[00:20:55 – 00:21:02] So basic, basic, basic behavior, but there's a trajectory there, right? If I'm slightly late.
[00:21:02 – 00:21:03] Suddenly
[00:21:03 – 00:21:05] You know, I become less reliable.
[00:21:05 – 00:21:11] Now, if I'm less reliable, people around me don't trust me as much. If they don't trust me as much,
[00:21:11 – 00:21:19] I start disconnecting, or they disconnect from me. And then all of a sudden, things start to collapse. So, if I have to call my head of sales and he doesn't answer me.
[00:21:20 – 00:21:21] He's like, I'll call you later. Doesn't call later.
[00:21:22 – 00:21:24] I start going, why didn't you call me later?
[00:21:25 – 00:21:27] Then he's like, hey, sorry, I was busy. I'll call you soon.
[00:21:28 – 00:21:31] And we have a low sales day, unrelated. Just happened to have a low sales day.
[00:21:32 – 00:21:33] What does my brain start connecting?
[00:21:34 – 00:21:36] He's off, so therefore sales are off.
[00:21:36 – 00:21:38] Right. I have no other way to associate it.
[00:21:39 – 00:21:47] So it's so important that everyone on the team, even my team, they know I need consistency. I even give everyone a schedule. I'm calling you exactly at this time today.
[00:21:47 – 00:21:57] Right. There's a weekly schedule. Everyone knows when they're going to be on a conversation with me. This way, we know if someone didn't show up to that conversation, it's because they are deviating from a baseline.
[00:21:57 – 00:22:03] It's very simple when you build the structure, right? Same with my routine. If I sleep at the same time every day, no matter what.
[00:22:03 – 00:22:15] And I wake up at the same time every day, no matter what. And I eat at the same time every day, no matter what. And I work out at the same time every day, no matter what. I can very easily catch when I'm drifting from baseline. I find it to be crucial to be in a routine.
[00:22:16 – 00:22:20] Because otherwise you start drifting without realizing it.
[00:22:20 – 00:22:23] It's like driving your car. You're in a road. The road looks straight.
[00:22:23 – 00:22:32] So you look down, you let go of the wheel because you assume the car will go straight. And you look down and you start moving stuff around and you get back on the wheel and you realize you're in the other lane.
[00:22:33 – 00:22:34] Two lanes over.
[00:22:34 – 00:22:36] You thought you were going straight.
[00:22:36 – 00:22:42] But by the time you check, you have to correct massively because there's traffic coming on the other side. Who knows what's going on?
[00:22:42 – 00:22:43] The point is
[00:22:43 – 00:23:02] You don't want to have to overcorrect. You want to stay in your lane because the second you start drifting even a little bit out of the lane, you correct yourself back in the lane. Problem is, if you wait until you're completely in a different destination, you wait till you crash, you wait till something else happens, it's much more difficult to correct the behavior. So, even financially, I'm constantly predicting the market.
[00:23:02 – 00:23:14] I'm constantly predicting what's happening in the economy. I've done it to the point where, over the last eight years, Jack and I have compiled all our data, all our merchant data, all our sales data, how much we made, how many transactions we made, what the average
[00:23:14 – 00:23:18] uh customer value was per month at that time.
[00:23:18 – 00:23:21] and how many leads we got per that month.
[00:23:21 – 00:23:27] And it's actually, I mean, I don't know any other company that's like this. I mean, it's just kind of retarded, to be honest.
[00:23:28 – 00:23:29] But this is how our income looks.
[00:23:30 – 00:23:36] So if this is January, February, March, April, May, June, July, August, September, October, November, December, here's the income.
[00:23:39 – 00:23:40] Every year.
[00:23:41 – 00:23:44] That's how it looks. January is the slowest month.
[00:23:44 – 00:23:47] And it goes up every month. Now, here's something to note.
[00:23:48 – 00:23:52] If January is my slowest month and I have this entire quarter of the best month, what should I do?
[00:23:52 – 00:23:53] Well
[00:23:53 – 00:23:56] We add a seminar. We throw in limitless.
[00:23:57 – 00:23:59] Now limitless helps income.
[00:23:59 – 00:24:03] jump higher. Now we also know these months are a bit slower.
[00:24:03 – 00:24:05] So at limitless
[00:24:05 – 00:24:10] We sell Mental Millionaire. We sell all sorts of other events to try and stabilize the income.
[00:24:10 – 00:24:13] Right. Then, if I know these ones start getting really great.
[00:24:13 – 00:24:17] We start pushing events here. So all of a sudden, August.
[00:24:17 – 00:24:18] We have mindset mastery.
[00:24:19 – 00:24:37] Right, Mindset Mastery does well, diamond retreat does well, right? The more the harder thing to fill is mindset mastery, harder thing to fill is diamond retreat, right? It's 30k. So these are harder to fill. Well, if we push it out to this time of the year, it feels easier. Now you got Black Friday, November, right? You got all these things happening in these months. Well,
[00:24:37 – 00:24:55] We throw in seminar tickets back in for this. That's like an example. That's a very simple version, but we're constantly predicting what's going to happen. Now, sometimes there's fluctuations in the economy. Like right now, there are fluctuations in the economy. You notice gas prices are higher in California. Things are more expensive, right? We're in war and there's all this stuff going on. You go, all right.
[00:24:56 – 00:24:59] What's that mean? Depends. If the war is elongated,
[00:25:00 – 00:25:06] People will start running out of money. But if the war is short, which it seems like it's going to be pretty short, then
[00:25:07 – 00:25:13] Oil prices will drop, people will feel more confident, people will spend more. So we're pretty much prepared for both. How?
[00:25:14 – 00:25:30] Well, we're ramping up ads right now because there's still a lot of spenders going on right now. And we're doing that so we get a bunch of clients in the ecosystem. We know once clients are in the ecosystem, they stay with us for a long time. So, if acquisition of new clients becomes difficult, we're going to be able to overcome that. Also, next year, 2027.
[00:25:30 – 00:25:34] I have 40 out of 52 weeks of the year I'm on stage.
[00:25:34 – 00:25:51] Right. So, because we know AI is going to become a thing, we know it's going to be a pain in the ass. I'm pushing even harder on the in-person events because people are going to crave that in-person connection and that want and that desire for one to be around people. So, we know that. So, we're already planning for that. How far ahead are you planning?
[00:25:51 – 00:26:04] In order to predict the baseline, like where is everyone's baseline going to change? I've been in business long enough to kind of know where the baseline might be going. So, you want to predict trends, you want to predict where trends are in your business. For example, my mom has a moving company. The only months my mom makes the most money.
[00:26:04 – 00:26:09] summer. Nobody's moving when there's snow outside, but they move over summer.
[00:26:09 – 00:26:17] So, summer now, throughout the summer, is the time everyone starts buying homes. That's the time everyone decides to move. So, her business is always booming in summer.
[00:26:18 – 00:26:22] So what does she do in summer? She hires way more people around now through summer.
[00:26:22 – 00:26:27] And she ramps up sales. So most of her revenue, she does like$3 or$4 million over the summer.
[00:26:27 – 00:26:31] And the rest of the year is very slow and she's just chilling. Maybe does a million dollars the rest of the year.
[00:26:32 – 00:26:45] Right, so that's how she runs her company. She ramps up during the summer. So, understanding the pattern, understanding the baseline allows you to leverage the situation. Now, if you know that a lot of people are going to run out of money, right, because of AI, a lot of people are going to be jobless.
[00:26:46 – 00:26:48] And you are a real estate developer.
[00:26:48 – 00:26:53] Well, the question is, when is your project going to be done? If it's done in 2027, fine.
[00:26:53 – 00:27:11] If you're thinking about a project that's done in 2028, 2029, 2030, you're going into riskier territory because now you don't know who's going to be able to buy or afford whatever it is you're doing, right? It's too far out. There's too much changing. It's too volatile, too unpredictable. What was once secure is no longer secure. For example, prior to COVID.
[00:27:11 – 00:27:13] What was one of the best real estate investments you can make?
[00:27:14 – 00:27:15] Commercial offices.
[00:27:16 – 00:27:18] Office spaces were literally the best investment you can make.
[00:27:19 – 00:27:20] Because businesses needed that.
[00:27:21 – 00:27:26] Now, San Francisco, over 80% of commercial buildings are empty.
[00:27:27 – 00:27:27] Why?
[00:27:28 – 00:27:29] Because everyone's on Zoom now.
[00:27:30 – 00:27:31] Right, I run my company from Zoom.
[00:27:32 – 00:27:35] I run my company straight out of my fucking laptop or my my phone.
[00:27:35 – 00:27:40] So understanding things change and they become unpredictable. Now,
[00:27:40 – 00:27:43] You know, another example of a shift in a pattern might be
[00:27:44 – 00:27:51] You miss a workout. Well, if you miss a workout, your brain, I this happened many times. I'll miss one workout, and then my brain goes, okay.
[00:27:51 – 00:27:53] Now that I've missed a workout.
[00:27:54 – 00:27:54] Yeah.
[00:27:55 – 00:27:56] What should I do?
[00:27:57 – 00:28:03] Ah, I'll miss one tomorrow. It's not a big deal. It's only two days, right? No big deal. I need to recover. I start rationalizing.
[00:28:03 – 00:28:05] Then I missed three days.
[00:28:05 – 00:28:06] Then I missed four days.
[00:28:07 – 00:28:08] Then I missed a week.
[00:28:08 – 00:28:09] Then I stopped working out.
[00:28:10 – 00:28:15] Right. So it make it no matter what I make it a thing. I'm not missing a workout.
[00:28:15 – 00:28:29] I have to not miss the workout. So you have to understand: predicting things is a superpower. It gives you, it lets you understand. Like, it's like, oh, if only I knew before, if only I knew about Bitcoin before. For example, I have a group, it's called the Cartel.
[00:28:31 – 00:28:35] Huh, it's like my one-on-one, like anyone my one-on-one clients, slash anyone who was in this group.
[00:28:36 – 00:28:38] I told them to short Bitcoin.
[00:28:39 – 00:28:40] At 126.
[00:28:41 – 00:28:47] They all knew about it at$126,400.$126,600 was the top.
[00:28:48 – 00:28:52] Everyone knew to short it at 126.4. I shorted it.
[00:28:52 – 00:28:54] Jack sorted it. My buddy Naeem sorted it.
[00:28:55 – 00:28:57] No one else listened.
[00:28:57 – 00:29:03] They didn't trust me. They were scared. Everyone was going up, right? They were like, no, we should not short it. No, no way.
[00:29:03 – 00:29:04] Well
[00:29:06 – 00:29:07] I was right.
[00:29:07 – 00:29:08] Why?
[00:29:08 – 00:29:15] Because I understand there's a pattern in trading. Trading is not that complicated. At least for me, it's not. The faster something goes up, the faster it comes down.
[00:29:15 – 00:29:24] Right, so you know when something is reaching a top because of two things: it starts rallying quickly, quickly, quickly, quickly, quickly. Like, it starts going faster and faster. I call it a frenzy.
[00:29:25 – 00:29:40] So if you look at the frenzy of fish going for food, right? They all jump on the food and it's just like a frenzy. Well, if they jump on the food, how much food is left? Not that much. So when you see the frenzy beginning, you know food's about to disappear. There's not gonna be any food left. Well, it's not gonna be any demand left either.
[00:29:41 – 00:29:50] So, as it starts to frenzy up, you know that they're about to pull the plug. So, I bet in the other direction. And vice versa, when there's a lot of food and there's no one eating.
[00:29:51 – 00:29:54] You know that it's a matter of time before people start eating.
[00:29:54 – 00:29:56] And there's there's too much food. People are going to need to eat it.
[00:29:56 – 00:30:03] So, you know that the tides are going to go the other way, right? So, everything's about patterns, everything. Now, you have to ask yourself.
[00:30:04 – 00:30:06] Based on my behavior, right? Your behavior.
[00:30:07 – 00:30:12] Where does this behavior usually lead to? If I walk in to my parents' house and I go, What's up, motherfuckers?
[00:30:13 – 00:30:13] Huh?
[00:30:13 – 00:30:14] What's up?
[00:30:15 – 00:30:16] Where's that going to lead to?
[00:30:16 – 00:30:18] A good relation with my parents?
[00:30:18 – 00:30:25] No, it's bullshit, right? If I tell my team, what's up, faggots? What's up, losers? I talk to them like that. What's that going to do?
[00:30:26 – 00:30:28] How how long before everyone decides to quit?
[00:30:29 – 00:30:30] A few days?
[00:30:31 – 00:30:32] Next.
[00:30:32 – 00:30:35] Right? So where where does the behavior lead to?
[00:30:35 – 00:30:40] Now, that's an extreme version, but there's always subtle versions, right? That's the harder one to catch. And
[00:30:41 – 00:30:42] Ask yourself if it's random.
[00:30:43 – 00:30:46] Is this just them having a bad day today or is it repeatable?
[00:30:47 – 00:30:48] Is this something they do all the time?
[00:30:49 – 00:30:55] If it's a bad day, all right, it's a bad day. But if it's a pattern that's about to repeat, you got to ask: where is this leading me?
[00:30:56 – 00:30:58] Where is this pattern leading me? It's very important.
[00:30:58 – 00:31:01] Now you have to also ask, is this an exception?
[00:31:02 – 00:31:04] Or is this revealing something? For example, I remember.
[00:31:05 – 00:31:06] I went to Europe.
[00:31:07 – 00:31:09] Uh with that girl I told you guys I was in love with.
[00:31:10 – 00:31:12] And she did cocaine.
[00:31:12 – 00:31:13] In front of me is
[00:31:14 – 00:31:14] at a club.
[00:31:15 – 00:31:17] And I called her mom and I told her.
[00:31:18 – 00:31:19] Von?
[00:31:19 – 00:31:20] Your daughter's about to be a drug addict.
[00:31:21 – 00:31:25] She goes, no, she's not. Now, I've seen people do drugs and they don't really touch it again.
[00:31:26 – 00:31:29] All of it is repulsive to me. However,
[00:31:29 – 00:31:31] I saw how she did it.
[00:31:31 – 00:31:33] And I saw what she how she acted on it.
[00:31:34 – 00:31:36] And I realized, I'm like, she's about to be addicted.
[00:31:36 – 00:31:38] Now that was in 2022.
[00:31:39 – 00:31:40] We're in 2026.
[00:31:40 – 00:31:41] She's still drug addict.
[00:31:42 – 00:31:44] Right. She's probably going to be for the rest of her life.
[00:31:45 – 00:31:46] Which is unfortunate.
[00:31:46 – 00:31:54] So much potential was one of the prettiest models in Israel. Was blowing up, had contracts with everyone, had contracts with Samsung, had contracts with everyone there.
[00:31:54 – 00:31:56] Decided to blow it. How?
[00:31:57 – 00:32:04] Getting into drugs. She just got into drugs, she threw away her entire future, right? Even with me, she threw away her future. She had me, she's never going to do better.
[00:32:04 – 00:32:12] Right. She had, in terms of income, she had herself made there. She could have been huge, huge. Everyone knew her.
[00:32:12 – 00:32:14] She threw it all in the trash.
[00:32:14 – 00:32:21] Why? Because she just wasn't there. But I saw the pattern. I got out. I said, I have to leave. This is going to, this is, I'm not going to get this to drag me down. I'm not going to do it.
[00:32:21 – 00:32:26] And that's what happened. She drags everyone down. Her parents are in massive debt trying to get her in rehab.
[00:32:27 – 00:32:35] It's very unfortunate. It's unfortunate, but that's what that's just selfish behavior. I saw the pattern. I said, I'm not going to be with someone selfish. It doesn't make sense to me. Right. So.
[00:32:35 – 00:32:38] Anytime you're going to correct a behavior, it has to happen early.
[00:32:38 – 00:32:43] The earlier you correct it, the easier it is to correct, right? When a train starts moving, okay.
[00:32:43 – 00:32:45] It's already difficult to stop.
[00:32:45 – 00:32:46] It's already very heavy.
[00:32:46 – 00:32:50] Even in moving at two miles an hour, the amount of momentum it carries.
[00:32:50 – 00:32:55] just that for the energy to get it to go two miles an hour, it'll still stop half a mile down the road.
[00:32:55 – 00:32:57] Right. It's ridiculous.
[00:32:57 – 00:33:01] So the question is, when do you correct it? Like yesterday I parked my car.
[00:33:02 – 00:33:04] My Lambo in a parking lot.
[00:33:05 – 00:33:17] And then normally, my car is if you push the off button, I created this habit because if you push the off button, car turns off, parking brake comes on, you have to think about it. I used to always put it in park and then put the parking brake on, right? I didn't know it just does it for me.
[00:33:18 – 00:33:20] So I turn off the Lamborghini.
[00:33:20 – 00:33:23] Assuming that the same shit happens in the Lamborghini.
[00:33:24 – 00:33:26] Turns out it's a neutral no parking brake.
[00:33:27 – 00:33:31] I go to get out of the car, I put my foot off the brake, car starts rolling. I
[00:33:31 – 00:33:36] Put my foot on the brake again. I'm like, are you kidding me? Right. So, when would it have been easier to stop the car?
[00:33:36 – 00:33:39] before I took my foot off the brake, put it in park, right?
[00:33:39 – 00:33:46] So, what happens if the car is going down a hill? What if I was on a big hill or something, right? So, it's just like you start thinking to yourself.
[00:33:46 – 00:33:59] Small things can lead to big, big, big income, like mistakes. So, that little error, if I had waited even maybe a half a second longer, my entire rear bumper and diffuser would have to be replaced. That would have cost me like$80,000.
[00:33:59 – 00:34:02] For no reason. For nothing. For a stupid mistake.
[00:34:03 – 00:34:08] Right. So understanding that little things have to be corrected early on.
[00:34:08 – 00:34:12] This is an example. So here's another example, right? I think that.
[00:34:13 – 00:34:15] If you have a small pattern, right?
[00:34:17 – 00:34:20] Once your identity gets attached to it, right? Once you have an identity there.
[00:34:26 – 00:34:28] It now becomes very difficult.
[00:34:30 – 00:34:31] to change the behavior.
[00:34:32 – 00:34:33] Here's why.
[00:34:34 – 00:34:37] Identity is expectation of your future.
[00:34:37 – 00:34:42] So to be happy, you have to remove all negative thoughts from your future.
[00:34:42 – 00:34:45] And all negative memories from your past.
[00:34:46 – 00:34:48] Now your identity is someone who things are going to be good.
[00:34:49 – 00:34:50] But it's hard to do that.
[00:34:50 – 00:34:55] If I start having a negative pattern, it's because I start believing there's going to be a negative future.
[00:34:56 – 00:34:59] So now I create a strategy internally where I'm less happy.
[00:34:59 – 00:35:00] And
[00:35:01 – 00:35:05] When that version of me is less happy, I start creating.
[00:35:05 – 00:35:08] a bad behavior. So at first it's a bad habit.
[00:35:09 – 00:35:12] Right. Then it become or bad behavior. Then it becomes a habit.
[00:35:12 – 00:35:17] Now, once saved, it's much harder to shift and change. Then it becomes an identity. So think of a smoker.
[00:35:18 – 00:35:19] Take a hit.
[00:35:19 – 00:35:21] They don't do it. It's just a behavior, bad behavior.
[00:35:22 – 00:35:28] You correct the behavior, they stop smoking, they don't smoke. You don't correct it, now they start smoking a couple of cigarettes a day. Now it's a habit.
[00:35:29 – 00:35:30] Now
[00:35:30 – 00:35:35] Someone goes, Hey, who you smoker? So I'm a smoker. Now it's an identity. Now they're a smoker for 40 years.
[00:35:36 – 00:35:38] Because it became an identity. Now it's
[00:35:39 – 00:35:40] Then it then it becomes
[00:35:41 – 00:35:41] You know
[00:35:42 – 00:35:43] That's just who I am.
[00:35:44 – 00:35:48] You know, my mom says that. That's just how things are. That's who I am. My mom's been smoking since she's a kid.
[00:35:48 – 00:35:50] She's sixty five. She's been smoking s since she's fifty.
[00:35:51 – 00:35:52] She doesn't want to quit.
[00:35:53 – 00:35:53] Just who I am.
[00:35:54 – 00:35:55] Right. It's become
[00:35:55 – 00:35:57] So deeply ingrained into her.
[00:35:58 – 00:36:00] It's much harder to make her quit now.
[00:36:00 – 00:36:02] than it was at the beginning.
[00:36:02 – 00:36:15] So I have to remove it. I have to get rid of that objection. It's not just who I am. I have to remove it from her identity, disassociate the two, right? For me to actually be able to get her acquit, I have to do a lot more work than if I just hit the cigarette out of her hand when she was a kid.
[00:36:16 – 00:36:17] Right, told her she's a fucking idiot.
[00:36:18 – 00:36:18] So
[00:36:19 – 00:36:21] You know, understanding that earlier the correction.
[00:36:22 – 00:36:31] There's less emotional resistance. There's less collateral damage. Okay. There really is damage when people do this. Like, my mom gets lung cancer. Think about the collateral damage that'll happen to my family.
[00:36:34 – 00:36:36] The stress will be catastrophic.
[00:36:36 – 00:36:40] The fact that she won't be at my wedding potentially.
[00:36:40 – 00:36:44] or see her grandkids catastrophic, right?
[00:36:44 – 00:36:45] And
[00:36:46 – 00:36:50] It's pretty bad. Now, why? Because she wants to smoke cigarettes. So.
[00:36:50 – 00:36:52] You know, understanding that when you do it early.
[00:36:52 – 00:37:04] There's less damage. There's less emotional resistance. There's less identity attachment. Less cleanup. It's just not as big of a deal. So, whenever you see something bad, this is why people might say, Marcel, you're overreacting early on.
[00:37:05 – 00:37:11] Anytime, like I told you guys, I had a relationship, my longest relationship. I finish work, I go back to my room.
[00:37:11 – 00:37:24] And my girlfriend's there and she's crying. And I go, why are you crying? I'm like, someone die? No. And I go, cool, I'm gonna go back downstairs to work some more. When I come back, if you're crying, you're not here or you're happy. One of the two. You decide which one.
[00:37:24 – 00:37:30] And I left. I came back. She was never unhappy again. I corrected the behavior at the very beginning of the relationship.
[00:37:30 – 00:37:35] Because I didn't want to encourage her being a victim, her being sad to get love and affection from me. So I didn't reward it.
[00:37:36 – 00:37:40] Rest of behavior. She was the happiest girl ever. Zero anxiety. Felt good the whole time.
[00:37:40 – 00:37:42] Why? But I corrected it early on.
[00:37:43 – 00:37:46] I didn't let it build up into, hey, you can't be like this anymore.
[00:37:46 – 00:37:51] Right, I didn't allow that to to drag on. And it's probably very good for her psychologically. Go ahead, Sabrina.
[00:37:53 – 00:38:00] So I'm curious what this is. Are you saying that the identity is um
[00:38:00 – 00:38:04] formed more by repetition or through that emotional experience.
[00:38:05 – 00:38:07] Our mind is always predicting the future.
[00:38:07 – 00:38:15] Your identity is based off of what you expect your future to be. If you think your future is, for example, you're going to have a family, kids, and be a millionaire.
[00:38:15 – 00:38:31] Your current identity is based off of what you believe your future will be. If you think you'd be in great shape, then your current behavior changes to align with your future identity. If I keep doing bad things, my brain understands at some level unconsciously that I'm going in a bad direction. So now my identity becomes a shitty outcome.
[00:38:32 – 00:38:33] My shitty future.
[00:38:33 – 00:38:38] And now, once I believe that, it's much harder to make me believe that things will be better.
[00:38:38 – 00:38:43] If I believe that my life will not be good, it's much harder to change that than it is to just.
[00:38:43 – 00:38:47] correct it before I let my mind even start predicting a negative outcome for myself.
[00:38:47 – 00:38:48] Right.
[00:38:48 – 00:38:49] Think that
[00:38:50 – 00:38:51] Now
[00:38:52 – 00:39:01] Here's the big one. This is very important, okay? Why am I so consistent? Because I have actual feedback loops built into every area of my life. I wake up in the morning.
[00:39:02 – 00:39:08] I take a piss. I jump in the shower. I get out of the shower. I take the towel off once I'm dry. I open up the weight.
[00:39:08 – 00:39:10] Uh like my weight
[00:39:10 – 00:39:11] My scale app.
[00:39:12 – 00:39:15] I get on the scale and I see my weight show up on my phone.
[00:39:15 – 00:39:24] And that tells me where I'm at on my diet. Am I following the right trend? Am I heading in the right direction? Is my scale going down or not?
[00:39:24 – 00:39:25] Now.
[00:39:26 – 00:39:29] If it goes up for multiple days in a row.
[00:39:29 – 00:39:31] I know I must be doing something wrong.
[00:39:31 – 00:39:33] There must be something I'm doing wrong.
[00:39:33 – 00:39:39] So there's a feedback loop. I need to dial in my diet. I need to do more activity. I need to figure out why I'm not losing weight.
[00:39:40 – 00:39:42] If I'm going down, down, down.
[00:39:43 – 00:39:44] I know things are locked in.
[00:39:44 – 00:39:52] Right. So you have to understand there's a feedback loop even when I wake up. Next thing I do is I look at my end-of-day report. I have an end-of-day report at midnight that's sent to me.
[00:39:52 – 00:40:03] When I wake up, as soon as I get off the scale, I look at my individual report. How did we do yesterday? Why didn't we hit our numbers? Or if we did, what was working? I then go look. I'm like, okay, here's what's going on. Here's what we got to focus on today.
[00:40:03 – 00:40:04] Fantastic.
[00:40:04 – 00:40:07] Now I know what's going on. Now I know what I need to focus on.
[00:40:08 – 00:40:23] My brain goes, okay, now I understand the metrics. What do I have to focus on in my company today? What are we behind on? What tasks aren't complete yet? What are our goals for the month? For example, filling the seminar in Miami, et cetera. Feedback loop on all the numbers, where we're at. Then I'm like, okay, here's what I have to do today.
[00:40:24 – 00:40:27] Then I get up, I go to the gym.
[00:40:27 – 00:40:40] I know on my notes app how much weight I have to lift for every workout. I have the same routine, how much weight I'm lifting everything. If I'm keeping my strength or getting stronger, I know I'm doing a good job. If I start losing strength, I know that something's off.
[00:40:40 – 00:40:50] I'm losing too much muscle. I have to up the amount of protein I'm eating. Right. So I'm extremely in tune with the feedback loop. If I ask someone to hang out with me, like I want to go on a date.
[00:40:50 – 00:40:58] And suddenly they're not reliable. They're inconsistent. They're late. They don't show up. These are all red flags to me. And I now say, okay, this is now unreliable.
[00:40:58 – 00:41:05] I have to remove things that are variables that are unreliable. I know that if we didn't hire two extra people this week that are trained.
[00:41:05 – 00:41:09] We fucked up. I have many, many metrics that I measure my life on.
[00:41:09 – 00:41:15] And that's my constant feedback loop. I've done the math. I know exactly what I need to do to scale proportionally, consistently.
[00:41:16 – 00:41:18] The question is, are we on top of it or not?
[00:41:18 – 00:41:38] And I manage everything. Okay, here are my bills for the month. All right, cool. Take the money, put it in this account. Take this money, put in this account, take this money, put it in this account. Cool. Those are fine. How many months ahead are we? Right? Oh, we're a few months ahead. Fantastic. Oh, we're six months ahead. Fantastic. So I don't have to worry about this for six months. Now we can take some of the extra money and allocate it to investments or scaling or testing or something.
[00:41:38 – 00:41:55] Right. So it's all about understanding your mind and how do I take my situation and create a feedback loop that's actively showing me what needs to be done. Now, I want to also note something. If you have a company, you want to have an active feedback loop on your team's performance.
[00:41:56 – 00:41:57] How is my team behaving?
[00:41:57 – 00:42:05] What are they doing? And you want to build a system, a routine, like, okay, you can't rely on a kid to show up to school every day and follow his classes, right?
[00:42:06 – 00:42:07] But if you create periods.
[00:42:07 – 00:42:14] You create a bell that tells them when it's time to go to class, a location to show up to every day. They get punished for being late or tardy, right?
[00:42:14 – 00:42:18] They get rewarded for doing well and showing up on time and being a good student.
[00:42:19 – 00:42:23] You can get a baby to go and show up and be consistent. You can get a full grown adult to be consistent.
[00:42:24 – 00:42:30] Right. Especially if you hire someone who's already consistent. You know, why do people like actually hiring someone who's got a college education?
[00:42:34 – 00:42:36] They still got to get trained when they come to your company.
[00:42:36 – 00:42:44] They're still not talented, it's because they can follow instructions consistently. It's because they're able to pursue something long enough with enough consistency, it shows you their patterns.
[00:42:45 – 00:42:45] This is who they are.
[00:42:46 – 00:42:57] They're able to push past other people. They're able to finish it. They're able to actually outshine others and perform and they'll do well within my company. That's why they hire someone from Harvard, for example, because they know how competitive Harvard is to get into Harvard law.
[00:42:57 – 00:43:04] Right? It's hyper-competitive. So if I'm gonna get into Harvard Law, I must be exceptional in how hard I push it and how hard I work. Now,
[00:43:05 – 00:43:06] This is a big thing.
[00:43:06 – 00:43:18] You can't resort to like a big pattern that will blind you on this is self-judgment, right? I can't go in front of the mirror and be like, you fat piece of why am I so fat? I can't believe it. I can't, I can't do that.
[00:43:19 – 00:43:20] Okay, I gained weight on the scale.
[00:43:21 – 00:43:32] Gotta be logical, gotta be tactical. Why did I gain weight on the scale? What did I eat yesterday? Am I not counting calories correctly? Did my chef fuck up? Did I fuck up? I look at my steps. Did I hit my steps?
[00:43:32 – 00:43:34] No, I didn't hit my steps, right?
[00:43:34 – 00:43:36] So I asked myself, what is going on?
[00:43:37 – 00:43:40] Once I understand what is going on.
[00:43:40 – 00:43:50] I can correct it, but I have to have a baseline. Like I said, you guys got to know what your routine looks like. What is baseline? What does normal look like? And by the way, let me define normal for you.
[00:43:50 – 00:44:01] Normal should equal the result you're looking for. My normal, my actual baseline, not where my baseline's been, with the baseline I want to have. That's the normal I want you to define.
[00:44:01 – 00:44:14] Me losing weight, me making more, me improving my relationship. What does that baseline look like? Whenever I drift away from that normal, what can I do to keep me back in that normal? That's the psychology you want to be in. So you have to understand that.
[00:44:15 – 00:44:30] You want to develop a pattern, a level of pattern recognition. Okay. It's you're not, you don't want to be paranoid, right? You don't want to be hyper vigilant. Who, what did that say? You don't want to go into every word someone says. That's a waste of time. Okay. You don't want to assume the worst every time you talk to someone. That's also not good. But
[00:44:30 – 00:44:35] You want to observe clearly. You want to look at facts. What are the facts here?
[00:44:35 – 00:44:36] What are the facts?
[00:44:36 – 00:44:40] Right. And you want to compare it to baseline, especially your own baseline.
[00:44:40 – 00:44:46] Compare it to your baseline, right? And you want to notice: where are things repeating? What's the pattern? What can I predict here?
[00:44:46 – 00:44:48] What continuously happens, right?
[00:44:49 – 00:44:49] Then
[00:44:50 – 00:44:54] You want to interpret what's happening without your own.
[00:44:55 – 00:44:59] meaning attached to it. Like if someone, you know, let's say,
[00:45:00 – 00:45:01] Abraham, let's say you get busy, okay?
[00:45:02 – 00:45:04] You're a little bit too busy. You're stressed out right now.
[00:45:05 – 00:45:07] And you're not as warm the fire.
[00:45:08 – 00:45:10] She can't go say he doesn't love me.
[00:45:11 – 00:45:12] That's delusion.
[00:45:13 – 00:45:15] That becomes delusional interpretation.
[00:45:15 – 00:45:20] She has to recognize the pattern and understand with precision what is Abraham Field.
[00:45:20 – 00:45:22] Abraham is feeling stressed financially.
[00:45:22 – 00:45:25] Abraham needs a little bit more support. How do I offer him the support?
[00:45:25 – 00:45:42] Right? Bam. Now it's not about her, which is delusion. Now it's about understanding the pattern, and that creates homeostasis. So that's where pattern recognition comes in properly. The improper version is: he doesn't love me, prioritized work, doesn't care about me, all this shit. Now, what are you doing? You're encouraging a bad relationship. You're now.
[00:45:42 – 00:46:02] Now, what does Abraham do? Now, Abraham has to ask himself: do I want to reward that behavior while I have all this on my plate or not? He has two options: distance himself further, right? It actually creates the thing that you don't want. So, understanding the delusion oftentimes is what creates negative strategies. You want to be correct, not delusional. Now, there's a very, very, very, very, very important thing.
[00:46:02 – 00:46:04] There's a baseline and there's a spike, okay?
[00:46:05 – 00:46:06] Spikes are
[00:46:06 – 00:46:07] You know.
[00:46:08 – 00:46:15] Not necessarily a pattern. Not every off moment is necessarily a pattern. So is this like a one-off spike?
[00:46:15 – 00:46:20] Or is this a pattern that is becoming a trend? So it's going to become a normal thing.
[00:46:20 – 00:46:25] Right, if you have one bad day where you need more affection or attention, all good. Is it a pattern?
[00:46:25 – 00:46:31] Slash a trend, or is it just a one-off? Maybe she got some bad news or something and she needs more attention, right?
[00:46:32 – 00:46:33] Who knows? Now.
[00:46:33 – 00:46:34] Is it
[00:46:35 – 00:46:36] Emotion?
[00:46:36 – 00:46:37] For example
[00:46:37 – 00:46:41] Sometimes you feel something is off and it might not be off.
[00:46:41 – 00:46:48] Okay, some of you could feel off, but it's nothing to do with them. It's you, it's nothing to do with them, right?
[00:46:48 – 00:46:59] But or is it actual data? So you have to ask yourself: like, did something actually change? How many times has it changed? In what context did it change? Like, why did it change? If it did.
[00:46:59 – 00:47:06] Right, and then compared to what? Like, what's the baseline you're comparing this to? Or are you just feeling something's a little off? Right now.
[00:47:06 – 00:47:16] The biggest thing is when you correct, you don't want to overcorrect. Like, if I see I'm up on the scale, I'm not going to go from 1900 or 1800 or 1700 calories a day to 1300.
[00:47:16 – 00:47:17] Right?
[00:47:17 – 00:47:18] So
[00:47:20 – 00:47:21] What am I going to do instead?
[00:47:26 – 00:47:27] I'm going to observe where I'm at.
[00:47:28 – 00:47:40] Most people are extreme. They do a nuclear overcorrection, right? Someone has a little bit of bad attitude and they blow up on them. That's not where you want to be, okay? You want to understand that if someone starts slipping a little bit,
[00:47:40 – 00:47:43] You have a conversation. Hey, I see you're slipping a little bit. What's going on?
[00:47:44 – 00:48:00] You correct it, you don't overcorrect it. You don't go if you slip again, you're fired, right? It's not, it's never extreme because extreme means that you are not looking at it the way it is. It's kind of like you know, Iran shoots a rocket into Israel, and Israel shoots a fucking nuclear bomb back.
[00:48:01 – 00:48:06] Right. It's an overcorrection. That's not what you do. There has to be an appropriate response. Now,
[00:48:07 – 00:48:08] You know
[00:48:09 – 00:48:14] The biggest problem is most leaders, and this is where I see most people are bad. This is their Akilazil as a leader.
[00:48:16 – 00:48:17] They ignore it.
[00:48:17 – 00:48:18] They ignore the slip-up.
[00:48:19 – 00:48:25] Because it's not catastrophic. They only respond when it's catastrophic. This is, in my opinion, what a good leader does versus a bad leader.
[00:48:26 – 00:48:29] A good leader notices when there is a slip up and corrects it immediately.
[00:48:29 – 00:48:34] Keeps everyone on track. A bad leader waits until it's catastrophic.
[00:48:35 – 00:48:36] To respond.
[00:48:36 – 00:48:38] That is a mistake.
[00:48:38 – 00:48:42] It is actually a horrible mistake. Shows me that someone is not a good leader.
[00:48:43 – 00:48:59] You must correct early. So, you know, in a relationship, if someone's a little bit less transparent suddenly, they hide their phone a little bit, right? They're a bit less warm, they're a bit less consistent, then you know, most people don't do anything about it. They let it be. They just go, oh, whatever. I don't know why they're being this way, right?
[00:48:59 – 00:49:02] I go, what's up?
[00:49:03 – 00:49:04] What's up?
[00:49:04 – 00:49:05] You're late.
[00:49:06 – 00:49:09] You're not showing me your phone. You change your password. You're being weird.
[00:49:09 – 00:49:10] What's up?
[00:49:10 – 00:49:16] Most people wait till the betrayal hits or the breakup or a big conflict before they bring it up.
[00:49:16 – 00:49:18] I bring it up right away. You got to tell me what's going on.
[00:49:19 – 00:49:22] Oh, you were you were setting up a surprise birthday party for me? Thank you.
[00:49:23 – 00:49:24] My bad.
[00:49:24 – 00:49:26] But look, we're closer now.
[00:49:26 – 00:49:26] Right.
[00:49:28 – 00:49:29] But that's an example.
[00:49:29 – 00:49:31] So you don't want to let little things slip.
[00:49:32 – 00:49:35] I notice everything, but I try to understand before I react.
[00:49:36 – 00:49:40] I try to ask myself, is it emotion? Is it fact? Is it not fact?
[00:49:41 – 00:49:44] Right. So I observe, I take note, I understand.
[00:49:44 – 00:49:45] And then I decide, okay.
[00:49:46 – 00:49:48] Is this accurate or is this inaccurate?
[00:49:48 – 00:49:52] And then I go from there. Now, here's another example, right?
[00:49:52 – 00:49:54] There are things that keep you strong.
[00:49:55 – 00:50:00] You have a morning routine, you go to the gym, your food, right? Whatever it is, you have your own routine.
[00:50:02 – 00:50:04] If you stop doing any of these things.
[00:50:05 – 00:50:11] It often predicts that your identity is slipping, which means you're not focusing on outcome A, which is the good outcome, you're focusing on outcome B.
[00:50:12 – 00:50:13] Which is the bad outcome?
[00:50:14 – 00:50:15] And if you start slipping
[00:50:15 – 00:50:19] then you have to ask yourself where is this going right
[00:50:20 – 00:50:22] So I want to give you guys a
[00:50:22 – 00:50:24] framework okay
[00:50:24 – 00:50:25] Uh for this.
[00:50:25 – 00:50:26] And
[00:50:26 – 00:50:32] This is how you understand how to respond to patterns, okay, that you're noticing in yourself and in other people.
[00:50:32 – 00:50:33] So
[00:50:33 – 00:50:34] Let me write this down for you.
[00:50:38 – 00:50:40] So it's going to be five letters.
[00:50:48 – 00:50:49] Oh my gosh.
[00:50:54 – 00:50:55] Okay.
[00:50:55 – 00:50:56] So
[00:50:56 – 00:50:57] Peace.
[00:50:58 – 00:51:00] What does P stand for? It stands for pause.
[00:51:00 – 00:51:04] don't react emotionally. You pause, you take a second, you breathe, you understand what's going on.
[00:51:05 – 00:51:08] You observe, right? R, recognize.
[00:51:08 – 00:51:10] What pattern is repeating here?
[00:51:11 – 00:51:13] Have I seen this pattern in someone else?
[00:51:13 – 00:51:14] Is it happening elsewhere?
[00:51:15 – 00:51:15] Right?
[00:51:16 – 00:51:16] If
[00:51:17 – 00:51:18] Establish a baseline.
[00:51:19 – 00:51:21] What is the baseline for me or this person?
[00:51:22 – 00:51:27] Where is the baseline? Compared to what, right? This is a different behavior.
[00:51:27 – 00:51:28] Compared to what?
[00:51:29 – 00:51:32] You can't just say this is different. This could just be how they are.
[00:51:32 – 00:51:35] So compared to what is this a different behavior?
[00:51:35 – 00:51:40] Same time of day, before the eight, after the eight, right? There's a lot of reasons why someone might have a different behavior.
[00:51:40 – 00:51:43] Now you want to calculate trajectory.
[00:51:43 – 00:51:44] Where is this going?
[00:51:45 – 00:51:48] Right. Where does this lead if I let this keep happening?
[00:51:49 – 00:51:51] Or if this just keeps happening in general, where is this going to take them?
[00:51:52 – 00:51:53] Where is it going to take me?
[00:51:53 – 00:51:56] Right. So calculate trajectory, P-R-E-C.
[00:51:56 – 00:51:57] T
[00:51:58 – 00:51:58] Okay.
[00:51:59 – 00:52:00] Titan correction.
[00:52:02 – 00:52:03] What's small?
[00:52:03 – 00:52:05] Precise adjustment.
[00:52:06 – 00:52:07] can fix this right now.
[00:52:08 – 00:52:11] What small thing can I do that fixes this right now?
[00:52:12 – 00:52:12] Right.
[00:52:13 – 00:52:14] So you want to notice?
[00:52:14 – 00:52:15] You want to name it?
[00:52:16 – 00:52:21] The pattern, you want to predict it, you want to correct it, and then you want to track it. You want to get feedback seeing if it actually improved.
[00:52:21 – 00:52:22] Right.
[00:52:22 – 00:52:40] So, if you want to really win at a high level, guys, right? This is kind of like to wrap today. If you want to win at a very high level, you have to understand the pattern you have, other people's baselines, your own baseline, understand where there's a deviation, why there's a deviation, understand if you have to correct it or not correct it. If you wait till things become catastrophic, it's way too expensive and much harder to change.
[00:52:40 – 00:52:49] So everything is easy to fix when it starts shifting, right? You set the boundary at the beginning. If it's like, you know, you ever heard the saying: give someone an inch, they take a mile? No.
[00:52:49 – 00:52:52] Give someone an inch, what happens? They take another inch.
[00:52:52 – 00:52:53] You let it happen.
[00:52:53 – 00:52:58] Give someone another inch. Then they take a foot. You let it happen. Eventually they take a mile and then you overcorrect.
[00:52:59 – 00:53:02] Why didn't you correct it after the inch 1.1 inches?
[00:53:02 – 00:53:02] Right.
[00:53:03 – 00:53:04] Should have corrected there.
[00:53:04 – 00:53:13] But you didn't correct error, which is why they, this is why you eat shit, right? So correct things as they are. I'm very in tune with this because I know where things go.
[00:53:13 – 00:53:23] I understand the patterns. Anytime I see anyone, it's human nature to fall off a baseline. It's human nature to want more. It's human nature to ask or to be greedy or to take. It's human nature.
[00:53:23 – 00:53:31] The question is: as a leader, as someone who's responsible, as someone who understands patterns, can you correct the behavior and put it back on track?
[00:53:31 – 00:53:35] Some patterns are harder to put on track, but you should also look at your baseline.
[00:53:35 – 00:53:36] Where's my baseline?
[00:53:36 – 00:53:38] Right. And then awareness.
[00:53:38 – 00:53:57] You guys got to build the self-awareness. Self-awareness stems from where am I feeling? What am I feeling? Why am I feeling this? How does this feeling change my behavior? Where does this feeling come from? Right. It's really understanding: can I connect to my emotions? I know when I'm in the right mindset. I know when I'm in the right state. I know when I'm in the wrong state. And I know how to correct it. The first thing I correct before anything is how I feel.
[00:53:58 – 00:54:02] If I can correct that, I can correct everything else. But if I'm fighting my feelings.
[00:54:02 – 00:54:14] I'm not going to follow my routine. I'm eventually going to break. And once I break, it's hard to go back, right? So, in order to maintain my baseline, I must maintain my emotional baseline. You maintain your emotional baseline because everything comes from an emotion. Remember that, right?
[00:54:15 – 00:54:23] Then you'll be consistent. And then creating that emotional atmosphere for everyone around you that you need around you to be consistent. That's kind of the idea. Now, based on that, what questions do we have?
[00:54:25 – 00:54:25] Mm-hmm.
[00:54:29 – 00:54:29] If any.
[00:54:32 – 00:54:34] I'm in Miami next week.
[00:54:34 – 00:54:35] Uh 1 p.m.
[00:54:37 – 00:54:38] Probably to like six, seven every day.
[00:54:39 – 00:54:40] And then
[00:54:40 – 00:54:42] Owen will go after higher favorite.
[00:54:43 – 00:54:44] you know um
[00:54:44 – 00:54:45] But
[00:54:45 – 00:54:53] Yeah, one to 5:30, 1 to 6, Friday, Saturday, Sunday, especially your favorite days. You guys, I know you guys love Fridays, right?
[00:54:54 – 00:54:56] So if for some reason you want to make a four hour trip,
[00:54:57 – 00:55:04] You don't have to, but if you wanted to, you could. Anyone else who's in Florida wants to come, you guys are also welcome. Just let Jack know, he'll send you guys a ticket for free.
[00:55:05 – 00:55:09] My point, so there's a possibility they will come.
[00:55:09 – 00:55:15] Well, I mean, they're welcome. Anyone's welcome. Just let us know. We'll get everyone a ticket.
[00:55:15 – 00:55:16] The men
[00:55:16 – 00:55:19] Obviously we have diamond retreat coming up. We got the unspoken coming up.
[00:55:20 – 00:55:22] That's in May. That'll come up pretty quick.
[00:55:23 – 00:55:28] Jack, if you could start coordinating with everyone, make sure they get their rooms, their flights, all that good stuff.
[00:55:29 – 00:55:30] Obvious
[00:55:30 – 00:55:31] Go ahead.
[00:55:32 – 00:55:39] Um so facts versus emotions. I believe I get very emotional when I see the facts and they being ignored.
[00:55:40 – 00:55:42] That's right, so go look at that, those five letters.
[00:55:43 – 00:55:43] I do.
[00:55:44 – 00:55:45] What is the first one?
[00:55:45 – 00:55:47] And I do that all the time.
[00:55:47 – 00:55:54] And I predict from myself why I behave the way I behave because I know my baseline, but it gets very
[00:55:54 – 00:56:04] Dynamic based on the reaction that I give in front of me. Right. So you have to learn how not to rely on other people's reactions for your baseline. You have to learn how to be stoic.
[00:56:05 – 00:56:10] I'm not. That's where it is. I let you say that. That's why you have to learn how to be psoic.
[00:56:11 – 00:56:15] You can't let other people influence your emotional state.
[00:56:16 – 00:56:22] I'll give you an example. I sometimes get stressed from my team. Okay. My team will yell at me, they'll say shit to me.
[00:56:23 – 00:56:29] I don't really give a shit what they say. Like, you know, this is going to be hard for you to process because when I first came up with this, it was even hard for me to process, but.
[00:56:30 – 00:56:31] It makes a lot of sense now.
[00:56:32 – 00:56:37] If my dog barks at you and his intention is to tell you to get out of his chair or something.
[00:56:37 – 00:56:47] But he's like a little fucking Pomeranian, right? Like this cute little teacup Pomeranian. Like he's retarded, you know? And he's telling you, move, get out of my chair, but he's barking, okay? Like that thing is telling you what to do.
[00:56:48 – 00:56:48] Right?
[00:56:50 – 00:56:51] What does your brain tell you?
[00:56:52 – 00:56:57] Oh, he's telling me to move. Ah, you cry. No, you're just like, okay, that's just a dog barking.
[00:56:57 – 00:56:59] Right? Or that's just a bird chirping.
[00:57:00 – 00:57:02] It's just an animal making noise.
[00:57:02 – 00:57:04] So when people react this way,
[00:57:04 – 00:57:07] The proper way to look at it is it's just a dog barking or bird chirping.
[00:57:08 – 00:57:16] It's just noise. Like when I hear people talk to me, I'm not reacting to them. I react based on what I think they'll react to.
[00:57:16 – 00:57:17] But
[00:57:17 – 00:57:21] I just like a doctor, he sees blood, he doesn't care, I see emotions, I just view it as
[00:57:22 – 00:57:23] A pattern.
[00:57:23 – 00:57:24] I'm just watching the pattern.
[00:57:25 – 00:57:28] So I don't really care if they have to take out their anger on me, let them.
[00:57:29 – 00:57:30] And then I'll correct the behavior later.
[00:57:31 – 00:57:33] Because I know that the behavior is not productive.
[00:57:34 – 00:57:39] If my team yelled at me and made me 100K after because they felt guilty, I would make them yell at me every day, right?
[00:57:40 – 00:57:41] But
[00:57:41 – 00:57:42] Usually they yell.
[00:57:43 – 00:57:45] They build resentment and they make me less money.
[00:57:45 – 00:57:46] So
[00:57:47 – 00:57:48] That's not the solution.
[00:57:51 – 00:58:00] Go ahead. Well, what if you know that this whatever's happening, the the decision will be taken over a different way, different paths and it will affect our family.
[00:58:01 – 00:58:09] In that aspect, not just sleeping on me. That if you, no matter what, the best reaction.
[00:58:10 – 00:58:11] is always the stoic one.
[00:58:11 – 00:58:12] No matter what.
[00:58:14 – 00:58:16] It's always the calm one. Go ahead, Abraham.
[00:58:17 – 00:58:35] Question. I my wife has a beautiful awareness of everything around her and I think this is my part that I'm and lack a little bit a lot, not a little bit over there. I'm not engaged with the surround world. I was trained from a childhood to find a solution, be a leader as a a problem solver.
[00:58:35 – 00:58:51] And I'm so into my own zone that I'm not aware of what's going on around me and I'm not always predicting the things as they are doing that. By me it's come up with an instinct more sensing things in a different way. But I'm not. How can I pull pull myself to that direction?
[00:58:52 – 00:58:53] I think that
[00:58:54 – 00:58:57] There's got to be a balance, right? Yin and yang. Yes.
[00:58:58 – 00:59:00] I have a pretty good balance internally for both.
[00:59:00 – 00:59:06] I'm extremely aware of my environment, but I'm also aware of my emotion. You're very good at regulating yourself.
[00:59:06 – 00:59:07] She's not.
[00:59:08 – 00:59:17] So you could see what both extremes of the aisle look like, right? Extreme regulation, bad prediction of other people's behavior. Lack of regulation, hypervigilant, right?
[00:59:17 – 00:59:25] You have to learn how to both meet in the middle. So you can become more aware without letting it affect you. And she needs to be able to pay attention and let go without letting it affect her.
[00:59:28 – 00:59:34] But how do I do this? How do I shift it in my mind? Well, from now on, when you see me pick this up.
[00:59:34 – 00:59:35] And I take a sip.
[00:59:35 – 00:59:36] Ask why do you take a sip?
[00:59:37 – 00:59:38] It's toasted.
[00:59:38 – 00:59:39] Just ask.
[00:59:39 – 00:59:43] Maybe, maybe. Maybe I'm thirsty. Maybe I.
[00:59:43 – 00:59:45] Maybe I maybe you said something about, oh, you look fatter.
[00:59:46 – 00:59:50] And I got insecure, so I needed reassurance. So I took a sip of water trying to play it off.
[00:59:50 – 00:59:51] Good.
[00:59:51 – 00:59:53] Right. Like for example higher.
[00:59:54 – 00:59:58] You raised your hand. Well, Abraham, you raised your hand. Chai, continue talking and you do this.
[00:59:59 – 00:59:59] Mm.
[00:59:59 – 01:00:01] Right? Lid compression.
[01:00:01 – 01:00:05] Which means you wanted to say something, but you held back for a moment.
[01:00:05 – 01:00:08] So that's an example of body language that I'm aware of.
[01:00:09 – 01:00:10] Right? I see it.
[01:00:10 – 01:00:16] I see everything, right? Sabrina, I saw myself sip the water three times. Each time I did it, you picked up a can and drank.
[01:00:16 – 01:00:18] Right, so Sabrina's in big rapport with me, right?
[01:00:19 – 01:00:20] I see it.
[01:00:21 – 01:00:26] Doesn't mean I have to react to it. Doesn't mean I have to feel something towards it, but I take notes of all of it.
[01:00:26 – 01:00:27] Right.
[01:00:27 – 01:00:31] I'm extremely aware of my environment. Extremely.
[01:00:32 – 01:00:33] But I don't take everything to heart.
[01:00:34 – 01:00:35] This is the key.
[01:00:36 – 01:00:47] Okay, just because there it's like when you trade, right? If you're trading stocks, you see stocks go up or down, you don't go, oh my God, they're going up or down. You just go, okay, that's data. So Kaya, you have to look at it as data, not personal.
[01:00:47 – 01:00:49] In Abraham, you just have to look for more data, that's it.
[01:00:50 – 01:00:51] I think after the unspoken.
[01:00:52 – 01:00:53] In May?
[01:00:54 – 01:00:55] You will
[01:00:55 – 01:00:56] Very, very much.
[01:00:57 – 01:00:58] Have a shift in this behavior.
[01:01:00 – 01:01:03] Why? Because I'm giving you a lens on what to look at.
[01:01:03 – 01:01:05] And you'll find it fascinating and I think you'll like it.
[01:01:07 – 01:01:08] But that's some yeah.
[01:01:08 – 01:01:12] So look, a lot of it's a journey, right? Like, all of this stuff is just
[01:01:12 – 01:01:13] It's a mission.
[01:01:14 – 01:01:16] Right, everyone here is on a journey.
[01:01:16 – 01:01:32] So it, you know, sometimes we want things to happen immediately, but the mind is there's so many patterns, there's so much practice, it takes time. And one day you're going to wake up and you'll be like, oh shit, look, I really am different. But sometimes the change happens slowly. Like, you know, I'm down 20 pounds. Okay.
[01:01:33 – 01:01:34] I'm even down, I think
[01:01:35 – 01:01:36] I was 210 when you guys were here.
[01:01:37 – 01:01:38] I'm 197.
[01:01:38 – 01:01:42] Right. So I'm even down 13 pounds from when I saw you guys last.
[01:01:43 – 01:01:44] Even then.
[01:01:44 – 01:01:47] I look in the mirror and I go, Why am I not making progress?
[01:01:47 – 01:01:51] My mind is playing tricks on me, right? Like, I am much leaner than I was.
[01:01:51 – 01:01:54] Even then, my mind is trying to convince me that I'm not.
[01:01:54 – 01:01:55] Yeah.
[01:01:56 – 01:01:56] Right?
[01:01:57 – 01:01:57] Why?
[01:01:58 – 01:01:59] Because that's how the mind works.
[01:02:00 – 01:02:03] Right, we want the instant gratification. So, in my head, I'm like, dude.
[01:02:03 – 01:02:05] You don't give a fuck. You don't stop.
[01:02:05 – 01:02:06] This is just who you are.
[01:02:07 – 01:02:08] It's just my routine.
[01:02:08 – 01:02:14] And based on my routine, the rest will follow. That's how I am financially. I'm very patient financially, very patient.
[01:02:15 – 01:02:16] Even with social media.
[01:02:17 – 01:02:20] I didn't have more than 5,000 fucking subscribers.
[01:02:21 – 01:02:22] In 2022.
[01:02:23 – 01:02:25] I started my YouTube channel.
[01:02:25 – 01:02:28] in 2017. But even with those 5,000,
[01:02:28 – 01:02:30] I was doing about half a million a year on my YouTube channel.
[01:02:33 – 01:02:35] Now I have a hundred and twenty thousand.
[01:02:36 – 01:02:41] Last month I hit a hundred thousand. So suddenly I'm getting this exponential growth, 20% growth.
[01:02:42 – 01:02:43] In one month.
[01:02:44 – 01:02:47] It took me 2017 to now to 100K.
[01:02:49 – 01:02:50] February 1st.
[01:02:50 – 01:02:51] Here I'm in March.
[01:02:52 – 01:02:54] I'm up 20%.
[01:02:56 – 01:02:56] Well
[01:02:57 – 01:03:02] It happens like that. Patience, right? When do you see the biggest result like in your body, for example?
[01:03:04 – 01:03:05] So lots 2%.
[01:03:06 – 01:03:10] All right, the last few percent, you go from having no abs to being shredded.
[01:03:11 – 01:03:15] In business, you closed one big client, your entire income changes overnight.
[01:03:16 – 01:03:23] Right. That like my first million-dollar client, my first actually$20,000 client was a big shift for me. My first$30,000 client was a big shift for me.
[01:03:23 – 01:03:25] Because now I had a lot of money.
[01:03:26 – 01:03:27] I had the money to
[01:03:28 – 01:03:29] you know
[01:03:30 – 01:03:32] Buy a car one. I had the money to live in a mansion.
[01:03:33 – 01:03:35] I had the money to hire people suddenly.
[01:03:35 – 01:03:38] I could eat anywhere I wanted. I didn't have to worry about money as much.
[01:03:38 – 01:03:39] So
[01:03:39 – 01:03:42] A lot of this takes time.
[01:03:42 – 01:03:43] But then
[01:03:43 – 01:03:59] You get your big break. You wake up one day and the last layer of fat has literally disappeared and you're shredded. You know, you wake up one day and then everything just clicks in your brain. Everything is a result of consistency, right? Both good and bad. You wake up one day, everything's in flames.
[01:04:00 – 01:04:02] Well, it's because you didn't take care of everything.
[01:04:03 – 01:04:04] Should hit the fan.
[01:04:05 – 01:04:08] Vice versa, you wake up one day and you sell the company.
[01:04:09 – 01:04:14] And now, bam, you just made$100 million overnight. So there's always that.
[01:04:14 – 01:04:18] That thing going on, right? The question is, can I be consistent blindly?
[01:04:18 – 01:04:28] While being aware of what's going on, to make sure that we stay on entree. So, how do I make sure I have blinders on to where distractions that are not important, like words, don't matter? But
[01:04:29 – 01:04:34] If people are in the circle, they're in the road, they're in my lane, how do I get them in alignment with my mission?
[01:04:35 – 01:04:37] And make sure that they follow through and don't hold us back.
[01:04:38 – 01:04:43] Right. That's kind of the idea. Without taking too much emotion, without getting too reactive, just
[01:04:43 – 01:04:52] Being set on the mission. So that's the balance I think you guys got to work on. But I really do think, Abraham, like I had a lack of awareness as well. I tried, but I wasn't that aware.
[01:04:53 – 01:04:56] I learned a lot more when I learned a lot of this body language shit.
[01:04:56 – 01:04:58] It gave me a lot more awareness.
[01:05:00 – 01:05:03] Looking forward. Yeah, it'll be awesome. If you guys have questions for me, let me know.
[01:05:04 – 01:05:04] Um
[01:05:05 – 01:05:05] And then Kaya.
[01:05:06 – 01:05:07] Smack yourself.
[01:05:09 – 01:05:09] Do it.
[01:05:11 – 01:05:12] Do it.
[01:05:12 – 01:05:15] But what's for? So you snag yourself out of this mood, yeah.
[01:05:16 – 01:05:16] Yeah.
[01:05:17 – 01:05:20] Yeah.
[01:05:20 – 01:05:24] There you go. All right. Love you guys. I'll see you guys later.
[01:05:24 – 01:05:26] Thank you. Take care. Bye-bye. Bye, everyone.
