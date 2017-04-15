---
layout: post
title:  "Moderation guidelines for inclusive community"
date:   2017-04-15 10:25:19
categories: [community,discord]
comments: true
---
 &nbsp; My previous article [On the topic of moderation]({{ site.url }}/articles/2016-11/On-the-topic-of-moderation) was very Discord-specific. In this one I aim to address wider audience and focus on inclusion. What does that mean? I would like to express my Idea about moderating a large and diverse community, whether it's in an IRC chat, forum or mailing lists, in a way that will create safe environment for members of all shapes and colours. This is an important task especially in open source communities, such as the most important one to me, the Fedora community. I will be talking to _you_ assuming that you are the Community Manager (CM) responsible for setting the moderation guidelines in your community.

<!--more-->

### Moderation ideology

 &nbsp; I often refer to _"my Moderation Ideology"_ when I talk about this topic, so what does hide behind these words?

 &nbsp; **The idea of raising the community via discussion and explanation instead of removing the unwanted members.** You should not simply ban people for any offense if they are an actual member of your community (I'll mention an exception later.) The correct action would be to talk to them in the first place, explain what are they doing wrong, be their friend, their teacher who is trying to help. If whatever offense it is keeps happening, then proceed with punishment, with temporary bans and in the worst case permanent removal from the community. Use the tools to log every verbal action, so the rest of the team knows that they've been already _told off_ for this or that. **Do Not Threaten!!** Don't use threats, especially not in the initial discussion. You have to be their parent explaining why is it wrong what they've done.

 &nbsp; The exception to this ideology is intentional trolling or spamming. These people enjoy doing that, and have no interest in being a member of your community. Remove them permanently after careful consideration whether they are really this kind of a troll, or just extremely misunderstood user. You can often tell from a quick discussion.

### Moderation tools

 &nbsp; You can't do this without any tools. Just no, forget it. Either you need custom made tool, depending on the size of your community this can even play greater role in it than just mod-help. Or you can use something as simple as git tickets, mailing list with decent archives, wiki pages or other text collab tools.. I would advise having either custom solution, or well written generic solution. Avoid using pure text collaboration.

 &nbsp; I am working on a generic moderation support project, an ASP.NET Core web-application written in C# that will serve to keep track of moderation actions such as warnings or bans, will have good database search for users, and in later stage of development even a system for reporting users, ban appeals, etc...

### Core skills of a moderator

 &nbsp; Moderators should carry certain skills regardless of the community they moderate.

* Neutrality - the ability to separate personal feelings from the situation and objectively judge the conflict.
* Good written communication in the primary language of your community, without internet or technical slang or abbreviations. The moderator should be able to express themselves clearly and with precision, construct a logical argument and summarize the conflict in structured manner for better understanding of all parties involved.
* Transparency - every moderation action, every single verbal warning, everything should be logged using the tools of your choice. This will serve well in the future if the user repeats minor offenses, etc...
* Understanding and following the _"chain of command"_ - Moderators should be divided into regular ones, and something of a lead moderator (or a few in large large community) where the Lead Mod would handle the worse cases, moderation complaints and appeals, etc. It should never be the same moderator who is complained about, right? ;) 
* Good understanding of internal communication and transparency within the team using the tools of your choice.

### Taking an action

1. Calm down the situation in public, take it into private channel if necessary.
1. Talk to the people, don't just ban them.
1. Follow the ideology outlined by the CM.
1. Log your actions using whatever tools the CM or Admin provided.

### Inclusion

 &nbsp; In the ideal world everyone is equal, with equal rights, and equally treated by their peers. We should aspire to narrow the gap between that and the reality as much as possible. The moderation team is the front line of this fight, they first have to understand what does it mean. Moderators should use the above outlined approach to talk to people who cause problems, who make others feel lesser, et cetera. For example someone in a discussion just randomly says _"nah that code is gay,"_ the moderator should immediately step in with the words of wisdom, such as _"Please avoid homophobic slurs. If you don't like the code and by the looks of it, it's probably written by less experienced beginner programmer, why don't you help them learn instead? Add a little bit of the 'constructive' into your 'criticism' =)"_ Then they log telling the user off for _"jokingly saying that the code of another member is gay."_

 &nbsp; So what behavior is okay in an inclusive community, and what is not? These could be your public-facing rules:

1. Be respectful to others, do not start huge drama and arguments.
1. Hate speech, “doxxing,” or leaking personal information will not be tolerated. Free speech isn’t free of consequences.
1. Sexual harassment, even slightly suggesting anything gender biased is inappropriate. Yes, suggesting that women should be in the kitchen is sexual harassment. And we are not a dating service either.
1. Homophobic language or racial slurs are immature and you should not use them.
1. Do not post explicitly sexual, gore or otherwise disturbing content. This includes jokes and memes that have somewhat racist background.
1. Do not break the application and do not spam.
1. Respect the authority and do not troll moderators on duty. Do not impersonate Admins or Mods, or anyone else.
1. Use common sense together with everything above.

Further you should note how to proceed with reporting inappropriate behavior and how to file complaints about moderation or appeals - depends on your tooling.

### Thanks!

 &nbsp; Thank you for reading, feel free to comment below with your thoughts on the topic. Would you do something differently? Do you agree with me in the idea of trying to raise the community by explaining the problem and teaching better behavior?

