---
layout: post
title:  "Upgrading Fedora 24 to Fedora 25"
date:   2017-03-02 21:07:19
categories: [code]
comments: true
---
I've seen many sad stories and struggles when it comes to upgrading Fedora 24 to 25. I did not want to risk this while I had all kinds of conferences and responsibilities, however, today my `synergy` decided to not quite work properly. Funny enough, only half of my keyboard was working, some keys did not spawn the delicate letters. For this reason, I decided to upgrade to Fedora 25 now. I was thinking _"It's already broken, can't be worse right?"_

<!--more-->

And so I did it. A few simple keystrokes, two gigabytes of data downloaded, and here I am. Fedora 25 is up and running, without any issues. Even `synergy` is fixed \o/

{% include image.html
  img="assets/console-bunneh.png"
  title="Fedora 25 and the Console Bunneh"
  caption="Fedora 25 and the Console Bunneh"
  url="http://rhea-ayase.eu/assets/console-bunneh.png"
  align="center"
  float="false"
  border="1px"
%}

I did have but one conflicting package, that had to be _dealt with_ using the `--allowerasing` flag. This was actually the one for `synergy`, which I've got from copr. Anyway, glad I did it, no complaints so far. **=)**

There is a nice `Fedora Magazine` article describing the steps to upgrade your Fedora, if you haven't done so yet... [Just Do It!](https://fedoramagazine.org/upgrading-fedora-24-fedora-25/)

