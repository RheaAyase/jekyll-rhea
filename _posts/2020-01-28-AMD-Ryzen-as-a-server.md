---
layout: post
title:  "AMD Ryzen as a server - what's the catch?"
date:   2020-01-28 13:51:19
categories: [code]
comments: true
---

I spent too much money on AMD chips in the past few months. I built 4 new AMD based computers - 2600, 3600x, 3900x and 3950x. In this blog post I will focus on the last one, 3950x, which is in our home server. We run various open-source projects, hosting a few libvirt VMs for others, our nextcloud, but most of the resources are consumed by [Valkyrja](https://valkyrja.app) and it's [MariaDB](https://mariadb.org) database. We also run a few game servers - Minecraft, 7 Days to Die and more in the future. Feel free to join us on [discord.gg/fedora](https://discord.gg/fedora) **=)**

<!--more-->

#### Why AMD Ryzen as a server?

[3950x](https://en.wikichip.org/wiki/amd/ryzen_9/3950x) is great because it gives me the same number of cores as I had with the previous setup - dual Xeon - but nearly 4x higher multi-threaded performance and an insane boost in single threaded workloads. 3950x does not lose anything from its smaller siblings in this area, to the contrary, it's more powerful even for gaming. This is amazing for our use case of hosting both, typical server workloads and game servers for our community. Sure, you could go with Threadripper, but that's a bit out of our budget, and most certainly an overkill for our workloads. The below mentioned limitations would still apply though.

#### Where are the limits with Ryzen?


The limit is that AM4 can hold only up to 128GB of DDR4 memory. As long as you do not plan to exceed this number, you're good. Even better if you plan to stay under that, for example 64GB. I'll explain later. Another thing to consider is the Infinity Fabric and its clock (aka FCLK) which is limited to 1800MHz - above that you're overclocking. Going too far down is detrimental to the performance so we should stick to something between 1600 and 1800 MHz. This is tied to memory clock, and although you can decouple it, the benefits would be only with highly overclocked, or extremely slow memory. Let's not do that though =)

So we need 3200 to 3600 DDR4 (1600-1800MHz)

#### What’s the catch?

We can't just grab the best 3600 DDR4 we can find. Ryzen CPU's memory controller may not be able to handle that with 4 memory sticks. It's not a well known fact, there is a table floating around that one can use for guidance but I was not able to validate its source, so I won't include it here. It's pretty similar to what I list below though - it matches my own measurements.

#### What should we buy then?

So in the end, the best memory is G.Skill Trident Z Neo, with an alternative [Ripjaws V](https://www.gskill.com/product/165/184/1571734065/F4-3200C16Q-128GVKRipjaws-VDDR4-3200MHz-CL16-18-18-38-1.35V128GB-(4x32GB)) which is the same thing with different heatsink - it won’t fit under Noctua D15 setup.

{: .centered .striped .highlight}
| Capacity | Modules | Clock | Best product | Tested<sup>1</sup> |
|---:|---|:---|---|---|
| 32GB | 2x16 | 3600 | [F4-3600C16D-32GTZN](https://www.gskill.com/product/165/326/1562839473/F4-3600C16D-32GTZNTrident-Z-NeoDDR4-3600MHz-CL16-16-16-36-1.35V32GB-(2x16GB)) or [F4-3600C16D-32GTZNC](https://www.gskill.com/product/165/326/1562840211/F4-3600C16D-32GTZNCTrident-Z-NeoDDR4-3600MHz-CL16-19-19-39-1.35V32GB-(2x16GB)) | <input disabled type="checkbox" id="" checked=""> |
| 64GB | 4x16 | 3200 | [F4-3200C16Q-64GTZN](https://www.gskill.com/product/165/326/1562838981/F4-3200C16Q-64GTZNTrident-Z-NeoDDR4-3200MHz-CL16-18-18-38-1.35V64GB-(4x16GB)) | <input disabled type="checkbox" id=""> |
| 64GB | 2x32 | 3600<sup>2</sup> | [F4-3200C16D-64GTZN](https://www.gskill.com/product/165/326/1578906066/F4-3200C16D-64GTZNTrident-Z-NeoDDR4-3200MHz-CL16-18-18-38-1.35V64GB-(2x32GB))<sup>2</sup> | <input disabled type="checkbox" id="" checked=""> |
| 128GB | 4x32 | 3200 | [F4-3200C16Q-128GTZN](https://www.gskill.com/product/165/326/1578906135/F4-3200C16Q-128GTZNTrident-Z-NeoDDR4-3200MHz-CL16-18-18-38-1.35V128GB-(4x32GB)) | <input disabled type="checkbox" id="" checked=""> |

<sup>1</sup> I've personally tested most of these in our server, which is built on a budget Asus PRIME X570-Pro. Chances are that you could have better results and maybe take it another clock level up with 4 dimms if you would find a T-topology mainboard. Most of the regular consumer ones are Daisy Chain. It's also worth noting that I was not able to run 4x16 at 3000 on my 3900x without memtest failing really badly. This was very cheap Corsiar memory with pretty random ICs though. Don't buy those.

<sup>2</sup> Note that this is 2x32@3200 - at the time of writing this article there weren’t any 3600’s in this capacity available. G.Skill [announced](https://www.techpowerup.com/262342/g-skill-announces-new-ultra-low-latency-ddr4-32gb-module-kits) what may be a better option, however that is also 3200, just lower latency.

#### ECC?

Ryzen can actually run ECC memory. These however do not come in the same clocks and timings that we are talking about today. You can also enable sort of ECC on compatible mainboards with regular memory.

#### What about mainboard?

As I mentioned earlier, T-topology might be better for 4 dimms, however, these are extremely rare nowadays, and usually expensive. I have not tested these myself so I can not recommend it as worth the investment. My choice - Asus PRIME X570-Pro - meets my requirements for the price it's at. It has very good VRM to power this setup 24/7, not the worst intel network card (1gbps only) and it has some bios debugging capabilities (error LEDs.) Beware that the -P option comes with Realtek NIC and no debugging options. Save yourself the trouble and get -Pro =)

#### Conclusion

Ryzen 3000 is an amazing "revolution." Enjoy it. You can get some inspiration on my [pcpartpicker](https://pcpartpicker.com/user/RheaAyase/saved/#view=wBMjpg), or in [this Ryzen-hosted Nextcloud photo album](https://cloud.rhea.dev/s/qPjwdo9MCKFRR3S) ;)

