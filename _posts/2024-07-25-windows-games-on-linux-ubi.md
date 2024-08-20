---
layout: post
title:  "Installing Windows games on Linux - Ubisoft Connect"
date:   2024-08-20 00:31:19
categories: [code]
comments: true
---

You can easily run any Windows game on Linux nowadays without too much work. Let's look at an example - many Ubisoft games are exclusive to their launcher for at least a few months after release, if you have any of them on their Connect launcher, you might be interested in installing it on Linux, on your Steam Deck, or other gaming hardware.

<!--more-->

#### Ubisoft Connect

While I had issues with controls in Ubisoft games installed through Lutris, all of them run really well with Steam input, installed directly following these simple steps. You can use the same process for other windows game installers.

This process takes advantage of Steam and Proton to install windows applications. We will run the .exe installer through Steam to get it installed, then modify said install to be able to launch the installed product through Steam.

#### Installing Ubisoft Connect

1. If you're on SteamDeck (or other Steam gamemode session) make sure to switch to Desktop first :)
2. Download the launcher: [https://www.ubisoft.com/en-gb/ubisoft-connect/download](https://www.ubisoft.com/en-gb/ubisoft-connect/download)
3. Add it to Steam as a non-steam app (Menu -> Games -> Add a non-steam game to my Library)
4. Right click the added installer and go to its Properties -> Force the latest Proton version (at the time of writing 9.x)
5. Play -> it should now run the installer for Ubisoft Connect, follow the steps to install it. If the launcher automatically starts it at the end, close it.

We've now installed the launcher but we can't exactly execute it directly just yet. Let's sort that out:

1. Add to steam as non-steam app: `/home/deck/.steam/steam/steamapps/compatdata/<ID>/pfx/drive_c/Program Files (x86)/Ubisoft/Ubisoft Game Launcher/UbisoftConnect.exe`
  - Where you can sort it by date to see the most recently modified folder, that's probably it.
  - Note this `<ID>`, we will need it later.
  - If you're not on Steam Deck the `/home/deck` is gonna be different - that's your home folder and it will be your
    username.
2. Right click the added launcher and go to its Properties -> Force the latest proton version again (at the time of writing
   9.x)
3. Run it once and close it.
4. Now we have two `<ID>` folders at the path described above, one with above identified `<ID>` for the installer, and the newer one for the actual launcher.
  - You want to move entire `<ID>/pfx/drive_c/` from the installer `<ID>` we noted earlier to the launcher one. Verify you're moving the correct files - it should have the launcher.exe in it. We want it in the new "launcher" app folder. Once you are certain which one is which, I recommend you to delete the `drive_c` in the destination before cut&paste of the correct files.
5. Go to the Properties on the newer app yet again -> Fix the name, change the Target to the correct folder/launcher.exe as well as the Start In location.

You're done. Verify that it's functional! You can now run it, use it, install all the Ubisoft games you like, etc.

Cleanup and optional improvements:

1. Remove the installer app from your steam and you can delete it from your `~/Downloads` as well. And don't forget to sort your Dolphin by name again ;)
2. Optionally you can also add launch params to start the game of your choice right away, handy if you run only one game. However you should not be running the game .exe directly, do not add it as a new non-steam app, this would not work. Use the launcher.
3. Use the SteamGridDB Decky Plugin to change the artwork on Steam ;)

### Enjoy!

Find me in the [Fedora Linux Discord](https://discord.gg/fedora) if you have any issues or questions.

{% include image.html
  img="assets/gpd-ubi-lq.jpg"
  title="Ubisoft Connect running on GPD Win4 (Linux)"
  caption="Ubisoft Connect running on GPD Win4 (Linux)"
  url="https://rhea.dev/assets/gpd-ubi.jpg"
  align="center"
  float="false"
  border="1px"
  width="75%"
%}



