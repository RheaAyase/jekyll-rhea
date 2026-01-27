---
layout: post
title:  "Installing Windows games on Linux - Arknights: Endfield"
date:   2026-01-27 00:31:19
categories: [code]
comments: true
---

You can easily run any Windows game on Linux nowadays without too much work. Let's look at an example - Arknights: Endfield - using only Steam + Proton.

<!--more-->

#### Proton

I usually run things through `GE-Proton`, however this is the rare case when that has disappointed me. While the game installed fine for me and the launcher was semi functionaly, it wouldn't actually start the game.

So this time around, it's gonna be `dwproton` - installing it is pretty simple, grab `ProtonPlus` from flathub using your software center of convenience. Then simply run it and find dwproton in the list, hit install and you're done.

Make sure to restart Steam if you had it running.

#### Steam

1. If you're on SteamDeck (or other Steam gamemode session) make sure to switch to Desktop first.
2. Download the windows installer: [https://endfield.gryphline.com/en-us](https://endfield.gryphline.com/en-us) - bottom right corner of the page and I recommend you to immediately mute the tab in your browser ;)
3. Add it to Steam as a non-steam game (Menu -> Games -> Add a non-steam game to my Library)
4. Right click the added installer and go to its Properties -> Compatibility -> Force the use of `dwproton`.
5. Play -> it should now run the installer, follow the steps to install it, all the defaults are fine. If the launcher automatically starts it at the end, close it.

We've now installed the launcher but we can't exactly execute it directly just yet. Let's sort that out:

1. Right click the installer in steam again, this time we're gonna change the Target field to `"/home/deck/.steam/steam/steamapps/compatdata/<ID>/pfx/drive_c/Program Files/GRYPHLINK/Launcher.exe"`
  - You may have noticed the `<ID>` there - this is a generated ID for your non steam game and it's probably different from mine. To find out what it is, simply navigate to that location and take a look at which folder was modified last. That's the correct one.
  - If you're not on Steam Deck the `/home/deck` is gonna be different - that's your home folder and it will be your username.
  - And don't forget the quotes!
2. You're actually done now. It will work with gamescope, mangohud, or any other shenanigans that you're used to. Probably. Use the Launch options same as with any other Steam game.
3. Use the SteamGridDB Decky Plugin to change the artwork on Steam, or SDGBoop (flatpak) in combination with [steamgriddb.com](https://www.steamgriddb.com/search/logos?term=endfield)
4. Cleanup - you can now delete the installer.

### Enjoy!

Find me in the [Fedora Linux Discord](https://discord.gg/fedora) if you have any issues or questions.

{% include image.html
  img="assets/game-endfield-lq.jpg"
  title="Endfield on Fedora Linux"
  caption="Endfield on Fedora Linux"
  url="https://rhea.dev/assets/game-endfield.png"
  align="center"
  float="false"
  border="1px"
  width="75%"
%}



