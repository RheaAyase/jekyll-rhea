---
layout: post
title:  "On the topic of moderation"
date:   2016-11-13 10:25:19
categories: [community]
comments: true
---
### Terminology and the team

Moderation is very important part of community management. Let me begin by explaining these terms, so we understand what do I mean by what.

* **Community manager** is the one who makes the rules, who lights the path and guides the rest of the team. All the responsibility in any community falls onto the CM, whether it is responsibility for the moderation team, administrators, or even the state of the community and how happy the members are.
* **Moderators** are the footsoldiers of the community team, the first line of defense against bullies, trolls, spammers and alike. They are also the first point of contact of a member with the authority, and as such are responsible to relay the ideology to members and if necessary, they have to enforce the rules.
* **Admin** is often mis-used term in gaming communities, and people labeled _admin_ are often playing the role of the community manager. Admin merely provides the hardware/software for the community, and tools for the team, to make their job easier. I often use [Elite Dangerous Discord server](https://discord.gg/elite) as an example, and I'll use it in this case as well. I am an "admin" of the [ED Discord](https://discord.gg/elite), however, I am not only providing the tools (setting up permissions, roles and channels, keeping it running, and the [Botwinder](http://botwinder.info)), but I also laid down the rules, the moderation ideology, and I handle the worst cases - these are tasks of a CM, not that of an admin.

<!--more-->

### Moderation tools

 &nbsp; Lets assume that we do have somewhat decent tools to moderate effectively, for example the ability to take notes about members, the ability to keep track of who is who - if the system allows them to change their name, and we also need the ability to ban people temporarily, delete inappropriate messages, and maybe mute people. As I mentioned above, these tools would be provided by the admin, even implemented if the underlying system doesn't have them, just like I had to create [Botwinder](http://botwinder.info) for Discord.

 &nbsp; Now I'm going to be a moderator, with these tools to my disposal. I'm a happy moderator, and the rest of the team knows what is happening, therefor they are happy as well! =)
<br /> &nbsp; The system will keep track of all my actions every single time I kick or ban someone naughty, etc. This helps to keep track of who did what and how many times were they naughty, which is very important in large community. It will also help improve the communication in the mod team, by keeping track of these things - so the rest of the team knows what happened while they were sleeping. **Communication is the key to success.**

 &nbsp; Since I'm talking about the advantage of using the right tools right now, I should also mention spam-bots. We should use some kind of spam protection. Good spam protection will not only protect your server against spambots but it will also make sure to not tag a user as such by accident, this can be achieved by both having good enough measurement of what counts as a spam-bot (or just an asshole user who's spamming on purpose) and the other good way to prevent errors is to talk to the spammer. For example we can configure [Botwinder](http://botwinder.info) to remove duplicate messages, or remove certain specific kinds of links or all the links completely. Further we can configure it to automatically ban these people if tha spamming doesn't stop - after `n` messages. However, to make sure that we are not banning someone who is just a silly user trying to post something, the bot will PM them before it actually slams the hammer. See `Figure 1` for example of such message, or you can take a look at [this gif]({{ site.url }}/assets/botwinder-antispam-log.gif) to see logs of an actual case, where three spambots got banned and their spam was removed, before anyone even noticed.

{% include image.html
  img="assets/botwinder-antispam-pm.png"
  title="Example PM from Botwinder to s spammer"
  caption="Figure 1: Antispam bot PMing the spammer."
  url="http://rhea-ayase.eu/assets/botwinder-antispam-pm.png"
  align="center"
  float="false"
%}

### Moderators

 &nbsp; This should be obvious, but I'll mention it. Moderator should be level-headed person who is able to separate their personal feelings and objectively judge a situation. Further they should be able to talk and type clearly and use full sentences.

    {% raw %}
    cuz spking like..
    w/ wbz slang..
    cre8 hjuuuuuuuuuuge issUz
    {% endraw %}

 &nbsp; ...I'm sorry, i'm not too good at it :D Anyway, the point is that we need the user to clearly understand what is wrong. And even if they are not native speaker, using proper language helps translation, etc... Speaking clearly also helps differentiate between two different types of interaction with the community. Moderators are often members of the community and they want to socialize, have fun, and joke with people. If you joke with people using less formal language and formatting of your messages, and on the other hand you use well formatted sentences while _doing your job,_ you will clearly send the message that people should now respect your words. This effect can also by achieved by using _tools_, where the moderator can `op` themselves, assign themselves different chat colour that way, etc... You may know this from IRC, and [Botwinder](http://botwinder.info) can be configured to enforce this as well.

 &nbsp; An Ideal moderator would always try to talk to the user, explain the issue, explain what's wrong, why is it wrong, and give the user alternative to whatever are they doing wrong. Try to grow the community, don't just remove people without explaining what are they doing wrong. Maybe they do want to learn, grow, be a better person? It is also worth noting that the attitude of the moderator should be somewhat neutral, it should be neither hostile, nor too friendly, but don't be boring neutral either - they may consider you condescending, which is not entirely good either.

### Taking an action

 &nbsp; The right approach to dealing with naughty people would be to try and talk to them first (as described above) and only if that doesn't help and the user keeps repeating the same mistakes, they keep causing the same problems, then we should kick them out or ban them temporarily. However, even while kicking or banning people, we should let them know why. This can be improved by using the right tools again, another example from [Botwinder](http://botwinder.info):
<br /> Command `!ban @user 12h Posting inappropriate images and ignoring the authority.` will not only ban them for 12 hours and add a note to the user database, that the user was banned for 12 hours for _"posting inappropriate images and ignoring the authority,"_ but it will also PM the user with this message. See `Figure 2`.

{% include image.html
  img="assets/botwinder-ban-pm.png"
  title="Example PM from Botwinder to a banned user"
  caption="Figure 2: Notifying naughty user about a ban."
  url="http://rhea-ayase.eu/assets/botwinder-ban-pm.png"
  align="center"
  float="false"
%}

{% include image.html
  img="assets/botwinder-ban-log.png"
  title="Example log entry of a moderation action"
  caption="Figure 3: Automatically logging every moderation action."
  url="http://rhea-ayase.eu/assets/botwinder-ban-log.png"
  align="center"
  float="false"
%}

 &nbsp; As you can see I believe that people can change and improve their behavior, they just need some guidance. I think that talking to people is the key in this, but there are people who can't change, or don't want to change. People who think that they are better than others and the rules simply don't apply to them. In this case we have to establish who is the authority with a few temporary bans, however even that doesn't always work and in this case, they will have to be permanently removed from the community. These are the "more serious" cases that i mentioned in the beginning, where the Community Manager should have a chat with the rest of the team and decide whether to remove them for good, or try different approach.

 &nbsp; I should also mention, that there are also people who join places only to [troll](http://www.urbandictionary.com/define.php?term=trolling) and cause problems. I would just get rid of those permanently - they are easy enough to identify by just talking to them and observing what they have to say in return.

### Discord example

How do we approach a conflict on Discord, or similar chat-rooms?

* Let's imagine that there is a conflict between two or three users and they are very passionately arguing in your main chat channel, disturbing others.
* Say that they are unable to stop arguing when you tell them to drop it (for this example I will address you as a moderator)
* Now we could use some really good tool to force them to stop arguing, right? Let's use `!mute @user1 @user2 @user3` command to prevent them from talking in all your channels, while allowing them to enter a hidden channel.
* You've got their attention now, they are in a room with just you, and nobody else watching the argument anymore. You can now talk to them and see if you can achieve some kind of neutral solution, see if you can get them to agree about some middle-ground on the topic, etc...
* One of them is really mad? Well, he's now seriously insulting everyone around and even you. Ban them for an hour, for being disrespectful to authority - give them the time to chill.
* You can now unmute the chilled two members, or you can just let [Botwinder](http://botwinder.info) automatically unmute them in a few minutes.
* Last but not least, take yourself to a hidden channel and instruct the bot to add a note to the other two users as well, because verbal action is obviously not logged. You want to mention that they were involved in a conflict, but also that they did listen to you and moved on.

### Thanks!

 &nbsp; You made it this far, huh? Thank you for reading, feel free to comment below with your thoughts on the topic. Would you do something differently? Do you agree with me in the idea of trying to grow the community by talking to them?
