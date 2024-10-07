---
layout: post
title:  "Steam Deck experience on GPD Win 4 with Fedora Linux"
date:   2024-10-06 22:01:19
categories: [code]
comments: true
---

I tried other gaming oriented Linux distributions and found them all to be... well, to be frank, bloated. I don't need
Lutris preinstalled, I don't use it. Just like I don't need 20 other tools or launchers or managers installed, with
services running and draining my battery. Furthermore, I love the ability to simply "tab out" of my steam gamescope and
enjoy full desktop environment.

And so I've come to the conclusion, that the best thing I can do is to simply start from scratch. I've got [a little video](https://youtu.be/naxosj6NcGQ) showcasing what my install looks like, the below is the minimum you'd need to take care of to get something similar.

Note that this is about standard rpm based Fedora - **NOT Atomic Fedora** (NOT Silverblue/Kinoite/etc)

<!--more-->

## fsync-kernel

Most of the tools necessary to achieve this are already there. Some devices, including GPD Win 4 do benefit from enabling the [fsync kernel copr repository](https://copr.fedorainfracloud.org/coprs/sentry/kernel-fsync). In order to use it you need to:
- `$ sudo dnf copr enable sentry/kernel-fsync`
- Edit `/etc/yum.repos.d/fedora.repo` and `/etc/yum.repos.d/fedora-updates.repo`
  - Add `exclude=kernel*` to the main "[fedora]" and "[fedora-updates]" categories respectively
- You should be able to now simply `$ sudo dnf update --refresh` to grab the fsync kernel and reboot. Verify with `uname -a` or `rpm -qa | grep kernel` to see what you've got.
- Should the update above fail, for instance because Fedora has got a higher version, you can force it with `$ sudo dnf distro-sync kernel*`

## hhd

HandHeld Daemon provides various functionality necessary to run your handheld seamlessly, such as TDP limits, both through the decky integration as well as using the desktop UI. Installing it is quite simple - enable the [hhd-dev copr repository](https://copr.fedorainfracloud.org/coprs/hhd-dev/hhd/).
- `$ sudo dnf copr enable hhd-dev/hhd`

## Install all the things

Obviously we need steam and gamescope, both of which are already available. And hhd we enabled above.
- `$ sudo dnf install steam gamescope hhd hhd-ui`

## Executing steam in gamescope

I've got a little `.desktop` file in my taskbar that I use to run it. Shove it wherever you like, tldr this is what I run:
- `$ gamescope --mangoapp --steam --default-touch-mode 4 --hide-cursor-delay 2000 -f -W 1280 -H 720 -- steam -gamepadui -steamos3 -steampal -steamdeck -pipewire-dmabuf`
- As you can see I'm running mine at 720p even though my desktop is at 1080p. Ain't got no need for games to run higher.

My entire Desktop file is below, should you wish to benefit from a full copypasta... _(Note this contains my username. So fix it on your end!)_
```
[Desktop Entry]
Categories=Games
Comment[en_US]=Gamescope with fullscreen steam
Comment=Gamescope with fullscreen steam
Exec=gamescope --mangoapp --steam --default-touch-mode 4 --hide-cursor-delay 2000 -f -W 1280 -H 720 -- steam -gamepadui -steamos3 -steampal -steamdeck -pipewire-dmabuf -nointro
GenericName[en_US]=
GenericName=
Icon=steam
MimeType=
Name[en_US]=SteamGamescope
Name=SteamGamescope
Path=/home/rhea/.steam
StartupNotify=true
Terminal=false
TerminalOptions=
Type=Application
X-KDE-SubstituteUID=false
X-KDE-Username=
```

## Further tweaks

### Autologin your desktop session

We don't want login screens for deck-like experience. Note that you still need to use your password for sudo, etc. Again I'm on KDE so your configuration might varry a little bit if you're not.
- Settings -> Login Screen (SDDM) -> clicky the "behavior" button on top -> clicky the check box to automatically log in as your user, and your session.
- Create the nopasswwdlogin group and addyourself to it, and configure pam appropriately - follow the [Arch wiki for Passwordless login](https://wiki.archlinux.org/title/SDDM#Passwordless_login)

### Autostart gamescope

I use KDE, your configuration might differ. I simply __first__ created an autostart application in the KDE settings (search for autostart) and then replaced it with a link to my existing .desktop file:
- `$ ln -s ~/.local/share/plasma_icons/steam.desktop ~/.config/autostart/steam.desktop`

### Intro Video

I replaced the default deck startup video with a single black frame .webm here, as I haven't figured out a better way to get rid of it heh (`-nointro` cli argument doesn't seem to work)
- `~/.steam/root/config/uioverrides/movies/deck_startup.webm`

## Enjoy!

Find me in the [Fedora Linux Discord](https://discord.gg/fedora) if you have any issues or questions.

{% include image.html
  img="assets/gpd-battery-lq.jpg"
  title="GPD Win4 running Fedora Linux"
  caption="GPD Win4 running Fedora Linux"
  url="https://rhea.dev/assets/gpd-battery.png"
  align="center"
  float="false"
  border="1px"
  width="75%"
%}



