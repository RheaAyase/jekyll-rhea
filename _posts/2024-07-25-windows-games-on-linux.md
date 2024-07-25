---
layout: post
title:  "Virtual Reality"
date:   2024-07-25 17:01:19
categories: [code]
comments: true
---

You can easily run any Windows game on Linux nowadays without too much work. Let's look at an example - gatcha games - you won't find those on Steam. How would you go about installing it on Linux, on your Steam Deck, or other gaming hardware? You don't even need Lutris, but that is certainly an option if you use it. We're gonna look at using Steam's own functionality alone.

<!--more-->

#### HoYoPlay and Zenless Zone Zero

One of the most recent gatcha releases is Zenless Zone Zero game from HoYoVerse. This is the same folks behind Genshin
Impact and you can indeed install that or many other games this way. This process takes advantage of Steam and Proton to install
windows applications. We will run the .exe installer through Steam to get it installed, then modify said install to be
able to launch the installed product through Steam.

#### Installing HoYoPlay

HoYoPlay is their launcher through which you can install these games. Let's get to it:

1. If you're on SteamDeck (or other Steam gamemode session) make sure to switch to Desktop first :)
2. Download the launcher: [https://hoyoplay.hoyoverse.com](https://hoyoplay.hoyoverse.com)
3. Add to Steam as a non-steam app (Menu -> Games -> Add a non-steam game to my Library)
4. Rightclick the added installer and go to its Properties -> Force the latest Proton version (at the time of writing 9.x)
5. Play -> it should now run the installer for HoYoPlay, follow the steps to install it. If the launcher automatically starts it at the end, close it.

We've now installed the launcher but we can't exactly execute it directly just yet. Let's sort that out:

1. Add to steam as non-steam app: `/home/deck/.steam/steam/steamapps/compatdata/<ID>/pfx/drive_c/Program Files/HoYoPlay/launcher.exe`
  - Where you can sort it by date to see the most recently modified folder, that's probably it.
  - Note this `<ID>`, we will need it later.
  - If you're not on Steam Deck the `/home/deck` is gonna be different - that's your home folder and it will be your
    username.
2. Rightclick the added launcher and go to its Properties -> Force the latest proton version again (at the time of writing
   9.x)
3. Run it once and close it.
4. Now we have two `<ID>` folders at the path described above, one with above identified `<ID>` for the installer, and the newer one for the actual launcher.
  - You want to move entire `<ID>/pfx/drive_c/` from the installer `<ID>` we noted earlier to the launcher one. Verify you're moving the correct files - it should have the launcher.exe in it. We want it in the new "launcher" app folder. Once you are certain which one is which, I recommend you to delete the `drive_c` in the destination before cut&paste of the correct files.
5. Properties on the newer app -> Fix the name, change the Target to the correct folder/launcher.exe as well as the Start In location.

You're done. Verify that it's functional! You can now run it, use it, install your gatcha games, etc.

Cleanup and optional improvements:

1. Remove the installer app from your steam and you can delete it from your `~/Downloads` as well. And don't forget to sort your Dolphin by name again ;)
2. Optionally add launch param `--game=nap_global` which may or may not actually start the game. (At the time of writing this arg didn't actually work to directly update and start the game but that seems to be a bug.) You should not be running the game .exe directly, do not add it as a new non-steam app, this would not work. Use the HoYoPlay launcher.
3. Use the SteamGridDB Decky Plugin to change the artwork on Steam ;)

### Enjoy!

Find me in the Fedora Linux Discord if you have any issues or questions.

{% include image.html
  img="assets/gpd-hoyoplay-lq.jpg"
  title="HoYoPlay running on GPD Win4 (Linux)"
  caption="HoYoPlay running on GPD Win4 (Linux)"
  url="https://rhea.dev/assets/gpd-hoyoplay.jpg"
  align="right"
  float="false"
  border="1px"
  width="50%"
%}

{% include image.html
  img="assets/gpd-zzz-lq.jpg"
  title="ZZZ running on GPD Win4 (Linux)"
  caption="ZZZ running on GPD Win4 (Linux)"
  url="https://rhea.dev/assets/gpd-zzz.jpg"
  align="right"
  float="false"
  border="1px"
  width="50%"
%}


