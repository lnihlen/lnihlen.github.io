---
layout: post
title: "A Sunday of Gentoo"
date: 2018-08-26
tags: [ i_made_a_thing, personal ]
---

A Sunday on my own, awakened earlier than I probably would have slept on my own,
cup of coffee in hand, all set up on my new living room desk, Hil at work, the
dogs resting quietly on the couch. An opportunity for such a level of
undisturbed productivity is incredibly rare for me, like once-in-a-summer rare
for me.

So, rather than make any significant advances on the diverse projects I have
listed (within a mere 10 days!) on this site, I decided to install
[Gentoo](https://gentoo.org) on a workstation that had been laying disused for
some time after my last attempt to build it into a high-end gaming rig. I go
through gaming jags periodically, but with so little personal time to spare I
often feel the drive to *make something* with that time, and so recently my
video game systems have lain fallow.

I've put Gentoo on lot of systems over the years. It's a good way to get a
taste of the current state of affairs in open-source and Linux software. It
sorta feels like voting, too, in that you are exercising a right that you don't
do every day but is important, and actually more precarious than one might
hope. Installing Gentoo is exercising your right to build all of the software
you need to power a modern desktop computer from freely available source.

There's always a satisfying feeling, too, using command-line disk partitioning
tools to overwrite a Windows partition. That was actually the first surprise -
I used the old Windows install to write the ```iso``` image to a USB drive
using some tool called [Rufus](https://rufus.akeo.ie/). Rufus wanted to download
some additional files and add them to my image, which I found concerning. My
(entirely unresearched) guess is that this is some jazz related to Microsoft's
recent embrace of Linux. I'm glad that worked, however, since I used the booted
drive to clobber the old Windows partition. No going back to re-image that one.

Booting the iso was largely uneventful. You can tell how uphill a battle you are
facing by how much of your hardware works right from boot with the Gentoo
install image. Of course, the person who built that install image is way better
at Gentoo than I will ever be, so I've learned that the gap between a piece of
hardware working when I boot from the install to booting my own kernel can be
quite large, but at least the install image serves as a sort of existance proof.
Something like the fact that somewhere out in the world is a person who *could*
install Gentoo on this particular computer and have it work smoothly.

Kernel compile was largely drama-free, too, had to rebuild/reboot again and
aggressively include *every* Intel ethernet driver, not just the one supposedly
required to support my network card, but after that it came right up.

Then there was the business of the NVMe drive I'm using for the home directory
not being available soon enough during boot for automount to pick it up, so
adding the ```_netmount``` magic flag to my ```fstab``` options. Does that mean
if the network is offline during boot I won't mount ```/home```?

It's so nice logging in to a system with an empty home directory, none of
those awkwardly named "My Desktop" or other subdirectories hanging about,
presuming to clutter up your workspace with a bunch of assumptions about
how you would like to organize your files.

Ran into the first major speedbump when I started in on the install of the
Nvidia drivers for hardware-accelerated X. Got some noise about slot conflicts
with the ```ABI_X86``` not sure if the 64 bit or 32 bit versions of stuff should
be built. I first went with ```USE``` flags for both, got a little bit further,
and then had to switch back to only 64 bit builds.

Took the time during the build of X to work out. Started reading through lots
of different options for window managers. Another feature/challenge of Open
Source software being of course the diversity of options for that. Given the
glut of options I used recency of development as selection criteria and settled
on [awesome](https://github.com/awesomeWM/awesome/) window manager.

One build/install cycle later and I had awesome working on hardware-accelerated
X. Things got fun when I installed ```xdm``` and tried to get that working on
login. Black screen and a return to the ```xdm``` login screen. A dig through
the log messages shows the cryptic:

```
xdm: setproctitle not initialized, please either call setproctitle_init() or \
  link against libbsd-ctor.
```

I have some persistant error messages about lingering 32-bit libraries that
gentoo keeps thinking I need to clean up by re-emerging the nvidia drivers
but that doesn't fix it. Best guess is that some mixup in library builds
between 32 and 64 bit libs, but I can't seem to find a way to convince gentoo
to rebuild the libs dependent on the 32-bit stuff.

Before joining Hil for a late dinner at [Saturn](https://saturncafe.com/) I
kicked off the (well, the *almost*) nuclear option: ```emerge -e @world```, a
forced recompilation of every package installed on the computer.

And there's my Sunday, "squandered" on Gentoo, an uncertain fate for the future
of the project (although ```parted``` fixes all distro issues), no progress on
any of the various projects I had hoped to move forward. And yet I want to
install Gentoo on the laptop next. Putting Gentoo on laptops is even more
nightmarish - because of all the sophisticated behavior you expect from a laptop
in terms of state change from plugged to unplugged, lid closed to open, etc,
as well as all of the typically proprietary, closed source drivers required
to run all of that stuff. But there's something empowering about "reclaiming"
a computer by building and configuring it from scratch.

On the other hand, open source purists will wrinkle their nose at my use of the
closed Nivida drivers and, as soon as I have a working X system, you can bet
I'll be running Chrome, not Chromium, on there as well. All things in balance,
I guess.
