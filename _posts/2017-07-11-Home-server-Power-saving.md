---
layout: post
title:  "Home server: Power saving"
date:   2017-07-11 21:15:00
categories: [code]
comments: true
---
I was talking about setting up `RAID1` and deploying `Nextcloud` in my [previous post]({{ site.url }}articles/2017-07/Migrating-from-unRAID-to-Fedora). This time around I wanted to make it eat less power, since I'm gonna be running it 24/7. I used to shut it down when I knew I wasn't going to need it for longer time, especially in summer. So, here is what I did to make my home server eat less power, and generate less heat as well.

<!--more-->

#### BIOS

The first thing that I did was some BIOS tweaking. This PC used to by highly overclocked gaming desktop back in its days, it's power-hungry i7-2700K with 16GBs memory, an SSD and a bunch of HDDs. We've got 650W modular power supply unit from Corsair and water cooling combined with Noctua fans, which is an overkill for the current usage, but I'm not buying anything into it. It is what it is. The cooling is at least _really_ silent.

I did already lower the clock when I decommissioned the machine from primary desktop, but to my surprise, I found 4200MHz being the value even now. It used to be around 4.7 GHz if I remember correctly. So I just casually browsed BIOS and changed the following values:

* Disabled `TurboBoost` completely.
* Enabled `EPU` _This refers to [Asus EPU](http://event.asus.com/epu/) - so only if we have an Asus mainboard..._
* Disabled `Internal PLL Overvoltage`
* `CPU Voltage` - _I've set this back to Auto. I don't actually want to undervoltage it, I still need some performance._
* `CPU C1E`, `CPU C3 Report`, `CPU C6 Report` & `Package C State Support` - _These refer to CPU state reporting back to the OS which is fully supported by most OSes. This will significantly reduce power consumption, but introduce certain degree of lag when introducing some load. Higher C state, higher lag and power saving. [Ref &nbsp;<sup>1</sup>](http://www.hardwaresecrets.com/everything-you-need-to-know-about-the-cpu-c-states-power-saving-modes/)_
* Disabled `HD Audio Controller` - _Disable any other devices that we do not need..._

_I'm sorry but I know nothing about AMD tech..._

#### System settings

_We will run everything below as root, or sudo._

Now we need to figure out what else is waking our CPU up. This could be even stuff like connected HID devices such as mouse, so we need to pull these out if there are any, we have ssh for that! And you should totally unplug any optical devices if you're using any, not only they eat power directly, but cause your CPU to wake up.

##### C-states

So the first thing to check is our allowed C state, and raise it if they're disabled. [Ref <sup>2</sup>](https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7)
<br>`cat /sys/module/intel_idle/parameters/max_cstate` - This reports `9` in this case, which means that our bios settings will be accepted. _I didn't even know they go that high._ 

##### PowerTOP

`dnf install powertop` - There are many power management utilities, we can use a simple PowerTOP.
<br>`powertop --calibrate` - Install and calibrate powertop. This will take some time to run various tests to see how much power is your machine eating, which processes wake your processor up, etc...

When it's done, we will be presented with a table showing you how many times does your CPu wake up per second. See `Figure 1`.

{% include image.html
  img="assets/powertop1.png"
  title="Figure 1: PowerTOP - CPU wakeups"
  caption="Figure 1: PowerTOP - CPU wakeups"
  url="http://rhea-ayase.eu/assets/powertop1.png"
  align="center"
  float="false"
  border="1px"
%}

Here we are looking for anything that wakes up our CPU too much, and if possible, we will disable it. In this case, it is mostly taken by OpenShift and hrtimer - this stands for `High Resolution Timer` that we can't really disable, I would just recommend being on the latest Kernel. There were some really old bugs causing this one to go really high. Nothing else is running that we could shut down.

Use the `tab` key to browse, take a look at some interesting numbers. For example in you can see that our CPU is in the C6 state 85-90% of the time in `Figure 2`.

{% include image.html
  img="assets/powertop2.png"
  title="Figure 1: PowerTOP - CPU Idle stats"
  caption="Figure 1: PowerTOP - CPU Idle stats"
  url="http://rhea-ayase.eu/assets/powertop2.png"
  align="center"
  float="false"
  border="1px"
%}

We are interested in the last tab `Tuneables` (`Fig. 3`)

{% include image.html
  img="assets/powertop3.png"
  title="Figure 1: PowerTOP - Tuneables"
  caption="Figure 1: PowerTOP - Tuneables"
  url="http://rhea-ayase.eu/assets/powertop3.png"
  align="center"
  float="false"
  border="1px"
%}

As you can see there are _some_ badly tuned components. This means, that they could eat less power! We can either cherrypick through the list, create a list of commands to disable specific stuff when the PC boots, or just have it tuned automatically. We will be using auto-tune as it is nice and simple, and in this case the list it displays seems like it could all be tuned well, no suspicious components.

Create a new systemd unit file if it does not exist:
<br>`vim /lib/systemd/system/powertop.service` - The contents should be as follows:

```
[Unit]
Description=PowerTOP autotuner

[Service]
Type=oneshot
ExecStart=/usr/sbin/powertop --auto-tune

[Install]
WantedBy=multi-user.target
```

`systemctl enable --now powertop` - Now simply enable this service and run it.

##### Thanks!

I hope that this was useful post for someone, most of it will also apply to notebook users. If you are interested in very detailed guide to power management, I recommend reading the [RHEL Power Management Guide <sup>3</sup>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Power_Management_Guide/index.html)

#### A little tip

Did you ever run `vim` without sudo while editing a service, such as the above? Then you write all the things and only when you're done you will notice that you can't save it. Add this to your `~/.vimrc` file:
<br>`cmap w!! w !sudo tee >/dev/null %` - And now you can nicely save it using our cute _"write!!"_ `:w!!` command **:]**

---

Ref <sup>1</sup>: [Everything You Need to Know About the CPU C-States Power Saving Modes](http://www.hardwaresecrets.com/everything-you-need-to-know-about-the-cpu-c-states-power-saving-modes/)
<br>Ref <sup>2</sup>: [What are CPU "C-states" and how to disable them if needed?](https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7)
<br>Ref <sup>3</sup>: [RHEL Power Management Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Power_Management_Guide/index.html)

