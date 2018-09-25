---
layout: post
title: "SCLork Planning Meeting"
date: 2018-09-24
tags: [ personal, sclork ]
---

The lengthy rebuild of my desktop system after adding `pulseaudio` to my `USE`
flags completed sometime last night. This morning before work I rebooted but
got a straight up scary kernel panic on login. I had left some ALSA
configuration in place so after work, and a reboot after fsck, I remoted in to
the machine and removed that. Bit scary that some audio misconfiguration could
cause a kernel panic but the alternative is scarier, looking at `dmesg` there
were some warnings about a failure in the NVMe controller on the motherboard.
Spooky stuff. Let's assume that was collateral damage of the null pointer deref
that did occur somewhere in the audio driver, which was also logged.

I'm typing this on the workstation, seems stable so far (knock on wood). I
notice that with Pulseaudio working the Plasma IDE seems a lot more aware of
audio configuration, including Chrome working automatically with the Dangerous
Music Source without having to be told. And I got the `.jackdrc` file trick
working to get Supercollider (well, `scsynth`, turns out `supernova` doesn't
support this) to automatically boot `jackd` on server boot. But, of course,
the minute I boot `jackd` Chrome audio stops working. So, basically back where
I started, with perhaps an incrementally improved 

From a whole "choosing your battles" stand point I am trying to choose another
battle. We'll see how well I hold out. There's a
[FAQ](http://jackaudio.org/faq/pulseaudio_and_jack.html) on the jack website
that basically recommends that the simplest way to do this to use two sound
cards. That's pretty surprising to me, and kind of makes me determined to try
and discover a less ridiculous option.

I think sometimes with a computer running Gentoo, which offers so much control
and provides so many options, it feels a bit like a personal insult when I can't
get the software on this computer, which I have compiled almost entirely from
source, to cooperate with a simple thing like *having two applications make
sound at the same time*. Yes, it's more complicated than that, Chrome is closed
source and just wants to use ALSA, whereas supercollider is aimed for
low-latency audio and is part of a fleet of pro audio tools that are emerging on
Linux. But *wow*.

Last Monday I missed the first rehearsal of the SCLork ensemble while I was in
Chicago. So this afternoon I cut out of work a bit early to go catch up with
Bruno, the conductor, about the project. Bruno had one of his students hanging
out as well, and we tinkered with
[Utopia](https://github.com/muellmusik/Utopia). It has some networked clock
options which might serve useful to study for the tap tempo controller stuff
I keep meaning to get back to for my own supercollider personal project. We
didn't have great success in synchronizing clocks across laptops but I
hypothesized it could be because we were all on wireless networks. Next time
we're going to repeat the experiment using ethernet, to at least eliminate one
of the variables.

One of the things I've learned from
{% include tag_link.html tag="oort_cloud" %} is that I'm much more productive
and engaged with music projects when working in collaboration. So I'm excited
to see where we go with SCLork. Also, concert Theramin!


![Concert Theramin in SCLork rehearsal space]({{ "assets/img/blog/2018-09-24-1.png" | absolute_url }})


