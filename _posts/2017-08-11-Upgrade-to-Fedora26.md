---
layout: post
title:  "Upgrading Fedora 25 to Fedora 26"
date:   2017-08-11 14:37:19
categories: [code]
comments: true
---
Upgrading Linux workstation to a new version? Everything is going to break!!! O\_O
<br />...oh don't worry, it will be fine with Fedora =)

So here I am, upgrading my Fedora to 26 a month late again. I did not want to risk screwing it up just before [my talks]({{ site.url }}articles/2017-08/Microsoft-TechTalks-Brno). I'm finally free of anything stressful and have just regular work on my plate, I can do it now!

<!--more-->

##### Upgrading

It took a little over half an hour and nearly `2GBs` of downloaded date to get it upgraded. No issues, just one surprise when I started `weechat`. There were **two** buffer lists and some random errors printed in the middle of the chat screen.

##### Locale issue

One by one, from the random errors I can see that it's something to do with locale.

`locale -a | grep en` - quickly shows that I don't have `en_SE` in the list, this was the locale of my choice to get the right date and time format for Europe, and still keep it in English. I changed it `en_DK` which is what I'm looking for. Surprisingly this has nothing to do with Denmark, they just used that as a country code which has to be there, and `EU` could not be used for Europe.

The first problem solved.

##### Weechat issue

Weechat showing two almost identical lists of buffers? Turns out that they introduced new way to display the list of buffers, so now I have both of them active - `buffers` and `buflist`.

Quick search for [reference](https://weechat.org/files/doc/devel/weechat_user.en.html#buflist_plugin) on how to disable one of them, and typing it in.

`/set buflist.look.enabled false` - Second problem solved.

##### =)

Go and [upgrade your system](https://fedoramagazine.org/upgrading-fedora-25-fedora-26/) if you haven't done so yet. **=)**

{% include image.html
  img="assets/console-bunneh-26.png"
  title="Fedora 26 and the Console Bunneh"
  caption="Fedora 26 and the Console Bunneh"
  url="http://rhea-ayase.eu/assets/console-bunneh-26.png"
  align="center"
  float="false"
  border="1px"
%}

