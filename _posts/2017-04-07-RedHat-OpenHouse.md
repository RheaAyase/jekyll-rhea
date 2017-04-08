---
layout: post
title:  "Red Hat Open House Brno 2017 - aka rebinding my mouse buttons."
date:   2017-04-07 12:00:00
categories: [code]
comments: true
---
##### The day before...

I spent the last few days preparing for my upcoming _"Writing C# code on Linux"_ talk. I'm pretty confident that it's a good one, time to pack up my notebook and get ready for tomorrow. It's a few minutes past midnight and i need to get some sleep! Oh... if I do not use `synergy` from my desktop, my Logitech MX Anywhere2 mouse doesn't have the PageUp and PageDown buttons bound to its two extra buttons. I have to fix that, I want to use the mouse to flip slides...

<!--more-->

Okay so I will need to find out what mouse button it is...  
`rjanek@RedHat:~$ xev`

{% include image.html
  img="assets/openhouse-2017/xev.png"
  title="Running <code>xev</code> to find out what are the mouse buttons."
  caption="Running <code>xev</code> to find out what are the mouse buttons."
  url="http://rhea-ayase.eu/assets/openhouse-2017/xev.png"
  align="left"
  float="false"
  border="1px"
%}

So it seems that my mouse button that I would like to be PageDown is `Button 8` and the PageUp is `Button 9`. Now I'll need xbindkeys to make it happen...  
`rjanek@RedHat:~$ sudo dnf install xbindkeys xautomation -y`

...and now I'll create default configuration in my home directory:  
`rjanek@RedHat:~$ xbindkeys --defaults > .xbindkeysrc`

And to make my mouse buttons act like PageUp-&-Down I'll need to add two lines for each to the config, it's actually surprisingly simple.  

{% include image.html
  img="assets/openhouse-2017/xbindkeys.png"
  title="<code>.xbindkeysrc</code> configuration file"
  caption="<code>.xbindkeysrc</code> configuration file"
  url="http://rhea-ayase.eu/assets/openhouse-2017/xbindkeys.png"
  align="left"
  float="false"
  border="1px"
%}

And all done, I'll just add `xbindkeys` to my silly startup script and I'm done **=)**

##### _Zzz..._

It's over, I kinda survived but almost died in there! I was supposed to be in a smaller meeting room, but they exchanged me with someone else and I ended up in the bigger one for 24 people. Seems like there was 50 though!! So many people that the vent wasn't keeping up, and it was even noisy enough that I thought it will be a problem with _my voice._ **So Hot** I almost melted!

{% include image.html
  img="assets/openhouse-2017/photo-1-small.jpg"
  title="Attendees trying to squeeze into the meeting room..."
  caption="Attendees trying to squeeze into the meeting room... (credit: Lukas Musil)"
  url="http://rhea-ayase.eu/assets/openhouse-2017/photo-1-large.jpg"
  align="center"
  float="false"
  border="1px"
%}

My talk was about C# on Linux, I explained what is it .NET Core, and that it's awesome!  
_(Multi-platform, open-source and modular platform for server oriented applications.)_

I also touched on the available C# IDEs that people can use on Linux...  
* MonoDevelop - the good old mono IDE. Does not support .NET Core though.
* Eclipse with some [plugins](https://github.com/mickaelistria/aCute) - does not support .NET Core either (yet)
* Visual Studio Code - very plugin based IDE which I don't like **:D**
* JetBrains Rider - so far the only fully capable C# IDE out there! Supports all the things **`<3`**

{% include image.html
  img="assets/openhouse-2017/photo-2-small.jpg"
  title="Photo of Radka speaking - about to write some code"
  caption="Photo of Radka speaking - about to write some code (credit: Lukas Musil)"
  url="http://rhea-ayase.eu/assets/openhouse-2017/photo-2-large.jpg"
  align="center"
  float="false"
  border="1px"
%}

And I also wrote some code right there, I created a console application that was in my imagination managing _server side systemd services_, and then I added `Kestrel` dependency, the `ASP.NET Core` webserver and crafted it in but a few lines of code into very simple web API. At the last minute I deployed it all on RHEL in Azure, behind proper reverse proxy Apache httpd!

I almost died from heat. And I think that I've misjudged my audience and the talk was too technical...

_Thanks for the microphone!_

