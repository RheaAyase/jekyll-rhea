---
layout: post
title:  "Discord Guide: Server setup and Permissions"
date:   2016-12-20 11:25:19
categories: [discord]
comments: true
---
How to correctly set up Discord server and channel permissions?
<br />This guide assumes at least basic knowledge of Discord and server configuration.

You can watch a [video guide here](https://youtu.be/tFjA3DUoiPU)<sup> 2</sup> or continue reading this written guide.

<!--more-->

### Good channel structure
(video guide [00:00](https://youtu.be/tFjA3DUoiPU?t=0m00s))<sup> 2</sup>

I'll start with basic channel structure that will help keep things nice and clear on your server.

Channel types as shown in the [Fig.1](http://rhea-ayase.eu/assets/discord-guide-permissions/channels.png):
* Separators
* Information
* News
* Logs
* Staff
* Discussion
* Spam

{% include image.html
  img="assets/discord-guide-permissions/channels.png"
  title="Channel structure"
  caption="Figure 1: Channel structure"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/channels.png"
  align="left"
  float="false"
%}

You can of course structure your server differently, but this should give you basic idea of what works well. I personally usually list discussion channels first and info/news channels in the bottom, Jefi's Nest is a little bit of an exception to that.

##### Channel Separator

In the `l-------info-------l` channel separator you can see a list of _public_ info and news channels and brief description of each, similar list can also be found in the `l------chat------l` separator. I also added a list of roles here, to not clutter the `#info` channel too much. Less information and better structure often mean that the user will actually read it, although they very rarely do.

{% include image.html
  img="assets/discord-guide-permissions/channel-separator.png"
  title="Channel separator"
  caption="Figure 2: Example channel separator"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/channel-separator.png"
  align="center"
  float="false"
%}

##### Info

<u>Info channel should contain:</u>
* **Brief description** of the server - This would be just one or two sentences what the place is.
* **Rules** - Depending on the type of the community you might want to explicitly list all the insane ones. See [Fig.4](http://rhea-ayase.eu/assets/discord-guide-permissions/channel-info-rules.png) for example of something more than just "don't be an ass."
* **More detailed description** of the activities the user can participate in - In our case this would be some information about Botwinder<sup>[ 1](http://botwinder.info)</sup> and Overwatch. If you have a bot with Public Roles, just like our Overwatch, this is the place to list all of them, or any other services your bots provide.
* **Permanent invite link** - this is to prevent people from accidentally generating only temporary invite links and hanging those in public places. Simply take away their permission to do that and give them a nice permanent link.

{% include image.html
  img="assets/discord-guide-permissions/channel-info.png"
  title="Info channel"
  caption="Figure 3: Example info channel"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/channel-info.png"
  align="center"
  float="false"
%}

{% include image.html
  img="assets/discord-guide-permissions/channel-info-rules.png"
  title="Rules"
  caption="Figure 4: Example rules"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/channel-info-rules.png"
  align="center"
  float="false"
%}

##### News

Another read-only type of channels for public, where you or your staff will post the news about the server, community, activities and events, in case of gaming community maybe patchnotes and game updates, etc... In our case we have github updates with a bit of spam for instant updates about our project, and more importantly, `#botwinder-diary` which contains important news and notices.

##### Logs

Often hidden, sometimes public channels to be used by bots. There are all kinds of logs: edited/deleted messages, user joining/leaving the channel, moderation events like mute, kick or ban, and even administration events like editing or assigning roles. _(This will change sooner or later - see my article about upcoming [Discord update: Audit logs]({{site.url}}/articles/2016-12/Discord-update-Audit-logs))_

##### Staff

Hidden staff channels

##### Discussion

Discussion channels can be themed, for example in our case `#botwinder-help` is a dedicated channel for questions about Botwinder<sup>[ 1](http://botwinder.info)</sup> or other kinds of help with it, then we've got `#teh_code_-wat-` which is for code related discussions. Themed channels should be obvious what's the purpose form its name, and topic if necessary.

##### Spam

A simple spam-type of channel often called `#bot-playground`, `#memes` or `#offtopic`.

### Roles and permissions
(video guide [04:19](https://youtu.be/tFjA3DUoiPU?t=4m19s))<sup> 2</sup>

##### @everyone and member roles

The `@everyone` role is what _everyone_ has. This role should contain permissions that you want _everyone_ to have, such as reading messages and message history, sending messages, connecting and speaking on voice chat. ([Fig.5](http://rhea-ayase.eu/assets/discord-guide-permissions/roles-everyone.png))

If you use some kind of member or verified role that you assign to people when they speak up, or agree to rules, or maybe you use automated verification system for this, then I recommend not giving embedding, voice activation, reactions, nicknames, and other similar permissions to the `@everyone`, but instead save it for members only. ([Fig.6](http://rhea-ayase.eu/assets/discord-guide-permissions/roles-verified.png))

{% include image.html
  img="assets/discord-guide-permissions/roles-everyone.png"
  title="Role permissions"
  caption="Figure 5: <code>@everyone</code> role permissions"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/roles-everyone.png"
  align="center"
  float="false"
  border="1px"
%}

{% include image.html
  img="assets/discord-guide-permissions/roles-verified.png"
  title="Role permissions"
  caption="Figure 6: Member or verified role permissions"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/roles-verified.png"
  align="center"
  float="false"
  border="1px"
%}

##### Tag roles

Roles that serve as tags only, should have **no permissions** at all. See example `Overwatch` tag role in [Fig.7](http://rhea-ayase.eu/assets/discord-guide-permissions/roles-tag.png). Tags are often available to public via bot command, aka `Public Roles`, and as such you do not want people to be able to grab any permissions at all, not even the ones that are on the `@everyone` role.

{% include image.html
  img="assets/discord-guide-permissions/roles-tag.png"
  title="Role permissions"
  caption="Figure 7: Permissions of a tag role <code>Overwatch</code>"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/roles-tag.png"
  align="center"
  float="false"
  border="1px"
%}

##### Staff roles

Staff roles should be treated as more fancy tags that are not available to public, and should have no permissions, or only permissions needed for the staff. See example moderator role in [Fig.8](http://rhea-ayase.eu/assets/discord-guide-permissions/roles-moderator.png) which doesn't even have ban permissions, because we use a bot for that.

{% include image.html
  img="assets/discord-guide-permissions/roles-moderator.png"
  title="Role permissions"
  caption="Figure 8: Moderator permissions"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/roles-moderator.png"
  align="center"
  float="false"
  border="1px"
%}

### Channel permissions
(video guide [11:38](https://youtu.be/tFjA3DUoiPU?t=11m38s))<sup> 2</sup>

##### Discussion channels

Standard random discussion channels should have no permission overrides at all. You can create some Spam (refer to channel types) channels where you want everyone to be able to upload files and not just verified members, etc... but other than that, you should not explicitly give people permissions if they don't need them, if they already have them from server role permissions.

##### Read-only (info/news) channels

For read only channels you should just deny `Send Messages` permission on `@everyone` and then allow a staff role to post there (unless you want to handle this yourself, in which case you don't need anything else.)
<br />See [Fig.9](http://rhea-ayase.eu/assets/discord-guide-permissions/permissions-info-everyone.png) for an example.

{% include image.html
  img="assets/discord-guide-permissions/permissions-info-everyone.png"
  title="Channel permissions"
  caption="Figure 9: Read-only info channel permissions"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/permissions-info-everyone.png"
  align="center"
  float="false"
  border="1px"
%}

##### Hidden channels

Hidden channels, such a channel for moderators or staff, would have only a single permission denied from `@everyone`, which is to `Read Messages`, and then the `Staff` (or any other) role that you want to give access, should have the `Read Messages` permission explicitly allowed.
<br /> See [Fig.10](http://rhea-ayase.eu/assets/discord-guide-permissions/permissions-staff-everyone.png) and [Fig.11](http://rhea-ayase.eu/assets/discord-guide-permissions/permissions-staff-team.png) for examples.

{% include image.html
  img="assets/discord-guide-permissions/permissions-staff-everyone.png"
  title="Channel permissions"
  caption="Figure 10: Staff channel permissions - blocked <code>@everyone</code>"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/permissions-staff-everyone.png"
  align="center"
  float="false"
  border="1px"
%}

{% include image.html
  img="assets/discord-guide-permissions/permissions-staff-team.png"
  title="Channel permissions"
  caption="Figure 11: Staff channel permissions - Allowed role"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/permissions-staff-team.png"
  align="center"
  float="false"
  border="1px"
%}

##### <u>Wallpapering</u>
(video guide [13:42](https://youtu.be/tFjA3DUoiPU?t=13m42s))<sup> 2</sup>

Wallpapering is an act of making the whole channel permissions red, or green.
<br />**It is extremely wrong! Do Not Do That!!**

If you have staff role, set up permissions as explained above. Do not wallpaper it as shown in the [Fig.12](http://rhea-ayase.eu/assets/discord-guide-permissions/wallpaper-red.png) and [Fig.13](http://rhea-ayase.eu/assets/discord-guide-permissions/wallpaper-green.png)!

{% include image.html
  img="assets/discord-guide-permissions/wallpaper-red.png"
  title="Channel permissions"
  caption="Figure 12: Staff channel permissions - <b>incorrectly</b> blocked <code>@everyone</code> - <b><i>red wallpaper</i></b>"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/wallpaper-red.png"
  align="center"
  float="false"
  border="1px"
%}

{% include image.html
  img="assets/discord-guide-permissions/wallpaper-green.png"
  title="Channel permissions"
  caption="Figure 13: Staff channel permissions - <b>incorrectly</b> allowed role - <b><i>green wallpaper</i></b>"
  url="http://rhea-ayase.eu/assets/discord-guide-permissions/wallpaper-green.png"
  align="center"
  float="false"
  border="1px"
%}


##### Voice channels
(video guide [15:25](https://youtu.be/tFjA3DUoiPU?t=15m25s))<sup> 2</sup>

The last bit I would like to mention is voice channel for music bots. All you need is to simply apply already explained principle of minimal permissions necessary. I assume that the `@everyone` role has connect and speak permissions. All we need to do now, is to block this role from being able to speak, and adding a music bot (or its role) and allowing the `Speak` permission.

### Thanks!

Thank you for your patience, you made it this far! :D
<br />I hope that this guide was useful for it, feel free to ask questions or share your opinions and experiences in the comments below.

&nbsp;

_Read my other article [On the topic of Moderation]({{site.url}}/articles/2016-11/On-the-topic-of-moderation)._

------------

1) Botwinder: [http://botwinder.info](http://botwinder.info)
<br />
2) Please excuse my failing voice, I didn't have my best day (I have vocal cord disability)
