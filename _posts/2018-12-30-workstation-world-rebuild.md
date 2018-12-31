---
layout: post
title: "Workstation World Rebuild"
date: 2018-12-30
tags: [ personal, sclork ]
---

With the workstation build from yesterday booting on its own and showing some
signs of life on the hardware-accelerated Xorg build it was time to power it
down, finalize cable routing, attach the chassis panels, and install the
computer into its permanent location under my desk.

Of course, after bootup KDE isn't letting me log in, and the `dmesg` shows a
seqfault in ksplashqml segfault somewhere within Nvidia's libGLX shared library.
Googling around doesn't reveal anything super promising but I do remember that
during system build one thing I had done on my last computer to get it building
was to add a `ABI_X86="64"` line to my `/etc/portage/make.conf` file. So I had
done the same on this system as a matter of course. I had done that specifically
to respond to some ABI issues between the Nvidia drivers and the rest of the
system code. But forcing 64-bit builds on a multilib Gentoo system is probably
not wise as a default. I'm wondering if the segfault is some mismatch of 32 and
64-bit code resulting from the stuff I built and the proprietary code from
Nvidia. But `emerge` wasn't really picking up any KDE packages from the change
of ABI requirements back to defaults, just some fundamental stuff like
`ncurses`. So it was time for the mighty `emerge -e @world`, forcing a rebuild
of everything in the system.

The initial X install was a ~200 package build that took around an hour on this
(obviously disk bandwidth-limited) system. This one is a 710 package build so
I won't be holding my breath, I'm expecting it will take the better part of the
day.

This left me lots of time to laze around the house being sick as well as tinker
with the [SCLOrkClock Quark](https://github.com/lnihlen/SCLOrkClock) I've been
working on. I was able to write a good chunk of the preliminary documentation
and get the objects in to place. My hope is to do a test tomorrow on the laptop
server I've built, using the Quarks I have built.

I finished the documentation for the synchronized clocks, and then started
adding some of the code I had been roughing out for the remote controlled
clocks. Then I noticed that the package rebuild had completed back on the
workstation so switched gears to try and log in again to my shiny new system.

Curses, foiled again! Still getting that segfault within the nvidia-libGLX
shared object from ksqlashqml. Googling around uncovers a few other threads,
mostly from Arch Linux, with similar symptoms resolved by going back to an
older version of mesa. I'm still a bit fuzzy on the relationship between mesa
and the Nvidia drivers on a Gentoo box. Rather than trying that, however, my
next attempt was to try and upgrade the nvidia drivers to the absolute most
recent (masked) version, 415.25. On this version ksplashqml still crashes on
login, but it seems to be a recoverable crash and I was able to log in to my
system! Yay!

Now to really get heads down and finish up the SCLOrkClock work. Tomorrow's
really the last shot I have at it and I want everything to be working great.

Update: turns out it was just that I had forgotten to add my user to the `video`
group. Yeah. Oh well all's better now. But I still think I'm not turning that
splash screen back on.

