---
layout: post
title:  "AMD Ryzen - PBO, overclocking and undervolting"
date:   2020-03-25 18:51:19
categories: [code]
comments: true
---

Previously in what's becoming a Ryzen min-maxing series, we learned about [memory limitations](https://rhea.dev/articles/2020-01/AMD-Ryzen-as-a-server). This time around I'd like to introduce you to three different things that you can do with the clock and voltage. Tweaking PBO for gaming/workstation use, undervolting for server workloads, or overclocking to (not) destroy your processor.

No matter what you read here, go and enable XMP for your memory :D **BAM** 10% free performance right there.

<!--more-->

#### Terminology

{: .centered .striped .highlight}
||||
|---:|:---|:---|
| PBO | Precision Boost Overdrive ||
| OC | Overclock ||
| VRM | Voltage Regulator Module ||
| VCORE | VDDCR CPU voltage | The stuff we'll be talking about as just "voltage" |

#### PBO and the other alternatives

PBO (Precision Boost Overdrive) is essentially that thing that makes your Ryzen CPU boost above it's standard clock. Now if you google what it is, AMD describes it as a _"powerful new feature designed to improve multithreaded performance."_ That is far from truth, in fact, it boosts single to low-thread-count workloads much more than all-thread-count workload. In fact, you're gonna have much better high-thread-count performance if you disable PBO and set your clock manually to the maximum safe voltage. (More on that later.) However, this will decrease your single to low-thread-count performance. And as such we've got two main use-cases here.

* Workstation - Use tweaked PBO.
* Server - Use manual all core scalar. Some people call it "overclocking" but we're not really increasing the clock beyond what we would experience with PBO. We just fix it to that value.
  * Maxed out performance - use maximum **safe** voltage (We will learn about it below.)
  * Undervolting - use low voltage, and a bit lower clock. Recommended way to go for servers of any kind.

What happens if you run a heavy workload on a server with PBO enabled and stock? Well, take for example the Folding@Home initiative to fight COVID-19. They struggle with giving people work units, and if you split your CPU into multiple smaller workers, you will experience very high temperatures, too high to run 24/7. You should really undervolt it. Here is what I observed with a really good case airflow and Noctua D15 on my 3950X and 3900X alike.

**PBO Enabled**

{: .centered .striped .highlight}
| Workload | Temperature |
|---:|:---|
| All threads at 10% | 60°C |
| Single thread at 100% | 85°C |
| Half threads at 100% | 80°C |
| All threads at 100% | 70°C |

**PBO Disabled** - undervolted to 1.1V @ 4GHz

{: .centered .striped .highlight}
| Workload | Temperature |
|---:|:---|
| All threads at 10% | 45°C |
| Single thread at 100% | 52°C |
| Half threads at 100% | 65°C |
| All threads at 100% | 70°C |

**OC Max** would be similar to the above undervolting, just add `15°C` more to it.

As you can probably deduce without me, PBO is great for gaming and other workstation use. Not so much for severs.

#### PBO Tweaking

You can tweak PBO a little bit to gain a tiny bit more performance. Varies from chip to chip, it can be anywhere between 1% to 10% depending on workload.

You can follow Buildzoid's [guide on YouTube](https://youtu.be/0J3Iswsvdvc) but he rambles a lot so here is TLDR:

Find PBO settings in your bios and set it all to manual values:
  - PPT Limit: `300`
  - TDC Limit: `230`
  - EDC Limit: `230`
  - Scalar manual `4x`
  - Max boost clock `+200MHz`
  - Thermal throttle to your liking, I'm running with `85` but it never even hits `75°C` with my cooling.)

(Hint: it's in the AI-Tweaker section for Asus mainboards.)

#### OC - Maximum safe voltage (aka FIT voltage)

I like doing these things on _Winblows_, however it should be possible on Linux with some user experience differences. The tools should be available.

To find out what's the limit above which you should never go, keep PBO enabled, and grab some tools:

* [prime95](https://www.mersenne.org/download/#download)
* [hwinfo](https://www.fosshub.com/HWiNFO.html)

Now fire up prime95 with "small fft" and all of your threads. Next, assuming you're using _winblows gui_, in the bottom of the hwinfo sensors window you can click a little "reset min/max" button.

Let it cook for a few minutes. Your maximum voltage is called `CPU Core Voltage (SVI2 TFN)` - exceeding it even by a small amount will cause degradation over several months. Surprisingly AMD engineers with PhDs actually know what they're doing and the chip is already running at its maximum possible performance out of the box. This is why I said that it's not exactly overclocking, we don't want to break the chip.

#### OC Tweaking

And now the fun part. Don't actually push this with bad mainboards. Generally 450b chipset mainboards are not fit to run Ryzen 39xx - often even at stock they will cook their VRM struggling to power it. While on the other hand, pretty much all the X570 have good VRM and will be fine. You can consult [the mainboard mastersheet](https://docs.google.com/spreadsheets/d/1wmsTYK9Z3-jUX5LGRoFnsZYZiW1pfiDZnKCjaXyzd1o) or listen to Buildzoid [ramble about mainboards](https://www.youtube.com/watch?v=ti38JS8RuPU) (time table in the comments.)

If you really like to run Buildzoid's rambling on background, you can also check out this one on [chip degradation](https://www.youtube.com/watch?v=uMHUz16MuYA) _(He does say a few things wrong here and there, but ain't nobody perfect and the point stands.)_

Beware, stay away from SoC voltage. Leave it. Don't touch it. That's not what we're doing here. (SoC voltage drives APUs on chips that have them, and I/O die.)

##### Undervolting

Undervolting is simple - set some nice low voltage, and start at some reasonable all core multiplier. This varies from chip to chip of course, for 3950x you can start with `40.5x` at `1.15V` (Set vcore via offset (1.1V) `+0.05`)

Now you've gotta test it, as I said already I like to use _Winblows_ for this purpose, I use a few loops of `Intel Burn Test` on High. You can also use `stress-ng` on Linux but your mileage may vary. I noticed that it doesn't generate as much heat for example. (Around 10°C less)

If it's absolutely stable and you're happy with the temperature, you're done. If it ain't stable, decrease the clock by `0.25` ~ If it's stable but too hot, decrease voltage by `0.02`-ish

##### "Overclocking"

Now the other way around, eh? So let's take a bit higher values to begin with. Say `42x` and `1.2V`. (Again set vcore via offset (1.1V) `+0.1`)

Now test it the same way as with undervolting above. If it's unstable, increase voltage (while keeping it below our safe value.) If it's too hot, you've gotta decrease it or improve your cooling. If it's stable and you're nowhere near your maximum safe voltage, you can bump up the clock scalar by `0.25`

#### Have fun!

In the next blog post we will look at cooling and case airflow, and I will introduce you to my OCD workstation **:)**

