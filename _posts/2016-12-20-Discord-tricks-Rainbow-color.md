---
layout: post
title:  "Discord tricks: Rainbow color"
date:   2016-12-20 06:54:32
categories: [discord]
comments: true
---
Would you like to have a role on your server, that keeps changing colors? Keep on reading =)

### Set it up using Botwinder

1. Get [Botwinder<sup> 1</sup>](http://botwinder.info)
2. Configure it as you only wish, it's all on the website.
3. Now you need to create a new role: `!createRole roleName`
<br />~this will return `roleID` to be used later.
4. Create a new command timer in a hidden **spam channel** `!timer command 2016-12-20 18:10 1m !setColor roleID #hexColorCode1`
<br />~this will return `timerID` to be used later.
5. Add more random colours! `!timer randomAdd timerID "!setColor roleID #hexColorCode2"` etc etc...
6. Fix role hierarchy! Botwinder's role has to be above this new role, and yet you will need the new role to be above all other to overwrite their colours (or the other roles have to be default grey to be ignored)

See example [Fig.1]({{site.url}}/assets/discord-timer-color.png)

<!--more-->

{% include image.html
  img="assets/discord-timer-color.png"
  title="Example commands executed."
  caption="Figure 1: Commands used to create this in Jefi's Nest server"
  url="http://rhea-ayase.eu/assets/discord-timer-color.png"
  align="center"
  float="false"
  border="1px"
%}

Copy-pasta for your convenience **:**)
<br />Just don't forget to replace the `roleID` and `timerID` with what did the previous command spit out **:**p

```
!createRole SantaWinder

!timer command 2016-12-20 18:10 1m !setColor roleID #FF2727

!timer randomAdd timerID
"!setColor roleID #2730FF"
"!setColor roleID #27FFF6"
"!setColor roleID #E527FF"
"!setColor roleID #27FF41"
"!setColor roleID #FFF627"
"!setColor roleID #FF8627"
```

### Enjoy!

_Read my other [Discord articles]({{site.url}}/categories)._

------------

1) Botwinder: [http://botwinder.info](http://botwinder.info)

