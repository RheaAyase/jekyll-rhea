---
layout: post
title:  "Build a PC - Airflow"
date:   2020-04-13 01:11:11
categories: [code]
comments: true
---

Previously in our little PC building series of being bored during the human malware pandemic, we learned about [Ryzen PBO, OC, and undervolting](https://rhea.dev/articles/2020-03/AMD-Ryzen-PBO-OC-undervolting). This time around, let's deal with the heat that these things can produce!

Let's preface this with a disclaimer of what hardware I've built in the past. I went from AIO (All in one) liquid cooling about a decade ago, through custom loops back to AIO two years ago, and most recently went all-in with air cooling and as such I had to brush off some math, basics of thermodynamics and I've done a fair bit of real world experimenting to min-max the cooling of my various Ryzen chips. I'm also a big fan of [Noctua](https://noctua.at)

<!--more-->

#### Rules of the game

Generally speaking... these are a few main decisions that you need to make.

Rule #1 - water is always better than air. The biggest heatsink (Noctua D15) will perform as well as the worst AIO, when said AIO is paired with Noctua fans. If you use AIO with whatever fans it comes with, it's gonna be more noisy to achieve the same performance. That said, the difference between D15 and the best of large AIOs (360 or 280) is only a few degrees after the AIO achieves steady state (this is after the water warms up which can be quite a long time.) What's the bottom line? Liquid cooling is great for burst workloads, but after it warms up, it doesn't matter all that much.

Rule #2 - if you do not watercool GPU (and we're not talking about CPU-only server worloads) don't bother with it. Graphics card is gonna be decent 10-20° higher than the air cooled CPU and the CPU has a very easy airflow path, unlike GPUs, whether you use a rear or top exhaust.

Rule #3 - if you need reliability, forget water. Pump, soft pipe connections, ... A lot more variables that can go wrong.

#### Airflow

The thing that we're here to talk about. Airflow is what keeps your machine cool at the end of the day. You can have as big of a cooler as you want, if you can't dispose of the hot air that it produces in a closed box, it's useless.

Let's take a few things from the great book of physics. Where does hot air go? Up. How does dust get in? Through the intake _holes_. What prevents air from moving? Obviously walls. Airflow is decreased with every turn that it has to make. Airflow is decreased with every dust filter that you place in its path.

That's a good thing to talk about actually! Do you want dust in your I/O connectors? No? Then make sure to have **positive pressure** to ensure that all of the intake is through the dust filters, exactly where we want it. I find the ideal ratio of intake and exhaust airflow to be somewhere around 10-30% positive pressure, depending on what the intake situation looks like. For example if we have a very low case with little space underneath and it's gonna be on a carpet, with an intake fan, that intake will suffer. The same thing with many front panels - 90 degrees turn to get into the case, very small holes... One would say that in some of the more extreme situations it's even better to use pressure fans (those intended for use with liquid cooling radiators.) Now I encourage you to go browse [Noctua's page](https://noctua.at/en/products/fan) as they provide exactly how much airflow each fan will achieve at what RPM, and how much static pressure. Compare `NF-S12A FLX` with `NF-A12x25 FLX` - one has twice the static pressure of the other, at the cost of noise while keeping the airflow the same.

Another very important point to mention is, that bigger fans are always better. To simplify the difference, they're much much more quiet at the same levels of airflow and pressure.

The obvious - do not place the exhaust fan right next to the intake. You would want to blow through the whole case. If you have too much heat on your GPU and it's in horizontal layout across the whole depth of the case, you can even make a tiny hole under the GPU to get a bit of extra exhaust right around it by removing one of those pcie slot covers and using higher positive pressure - you'd want two fans on the front, and one in the back, with CPU heatsink pointing right at that back fan.

#### The ideal air cooling setup.

After many iterations of trying to achieve the best air cooling performance I came to the conclusion, that bottom-to-top _aero tunnel_ is the best setup possible. That is with CPU heatsink also oriented bottom-top and GPU positioned vertically in the dead center of the case (so that it's not right against the glass starving its own fans.) I have also added an extra 120mm ULN (Noctua thing - very low rpm silent fan) on intake to deal with all of the positive pressure. The bottom-up fans are four 140mm which results in theoretical `231m³/h` airflow in and out, with extra `57.5m³/h` for positive pressure. That's 25% positive pressure to account for proximity to the carpet, 90 degree turn under the case, and dust filters. From my observation I have not noticed any dust buildup anywhere on any holes on the case, or inside of the case, achieving _equilibrium_. (Too much of positive pressure can cause dust buildup within the case, but it's better than negative.)

Performance? Temperature? Well the temperature is the same as ever, since it's the performance what changes in modern AMD solutions, and not temperature. However, I can set my GPU to 150 MHz higher **overclock** while maintaining the same temperature and fan rpm/noise. I call that a win **;)** (That's 2150MHz on Radeon 5700XT) Oh and CPU is irrelevant as I said before, it's colder than GPU even when it's sucking the GPU heat right into its heatsink. My 3900x is almost never above 75°C

Here is what that looks like, I will let you be the judge of my OCD (I measured the fan distances to the fraction of a millimeter to line up exactly top above bottom, and exactly lined up with the graphics card.)

{% include image.html
  img="assets/skye.jpg"
  title="Skye Mk.II - Rhea's Desktop"
  caption="Skye Mk.II - Rhea's Desktop"
  url="http://rhea-ayase.eu/assets/skye.jpg"
  align="right"
  float="true"
  border="1px"
  width="50%"
%}

{: .centered .striped .highlight}
||||
|---:|:---|:---|
| Part | Component | Notes |
| Mainboard | Asus Prime X570-Pro ||
| CPU | AMD Ryzen 3900x | [blog](https://rhea.dev/articles/2020-03/AMD-Ryzen-PBO-OC-undervolting) |
| RAM | 2x16GB G.Skill Trident Z Neo 3600cl16 | [blog](https://rhea.dev/articles/2020-01/AMD-Ryzen-as-a-server) |
| Storage | Corsair MP 600 PCIe 4.0 ||
| GPU | Radeon RX 5700XT - Sapphire Nitro+ Special Edition ||
| GPU Vertical mount | cablemod.com ||
| Case | Lian Li PC-O11D XL ||
| CPU Cooler | Noctua D15 ||
| Main Case Fans | 4x Noctua A14 FLX | GPU-temp driven by Corsair Commander |
| Positive Pressure | 1x Noctua S12A ULN+LNA ||
| ..and more.. | [pcpartpicker.com](https://pcpartpicker.com/user/RheaAyase/saved/#view=NsGHBm) ||

#### Resources

When shopping, look up reviews. You don't have to use Noctua, but look up reviews, and use a bit of common sense **=)**

* [Gamers Nexus](https://www.youtube.com/GamersNexus) does great reviews of CPU coolers ([e.g. air vs water](https://www.youtube.com/watch?v=7VzXHUTqE7E))
* [Actually Hardcore Overclocking](https://www.youtube.com/ActuallyHardcoreOverclocking) Mainboard reviews ([e.g. timeline in the comments](https://www.youtube.com/watch?v=ti38JS8RuPU))

