---
layout: post
title: "Sick Day and Workstation Build"
date: 2018-12-28
tags: [ personal, vcsmc, sclork ]
---

I knew I would be tired after yesterday's trip to San Francisco but the cold I
had been incubating bloomed in to full flower overnight. You know you're screwed
when you wake up at 2 am because you're too sick to sleep comfortably. At least
I was able to dig up some NyQuil and try to bed down again for a few more hours
before our dog started her normal morning wakeup routine, which of course wakes
up the whole house.

A year or two back I had bought some parts to build a highly parallel
workstation machine for {% include tag_link.html tag="vcsmc" %} work. But I had
a lot of difficulty getting the machine to be stable with the RAM I had chosen,
then I got distracted by other things, so for a while these two very nice 18
core Xeon processors have been sitting around unused. Given my recent enjoyment
of having a powerful Linux workstation I'd been fantasizing about repurposing
those processors, by far the most expensive individual component in any
workstation I could afford to build, into a powerful desktop computer.

If I had a ton of money I wanted to invest in a workstation the obvious thing
would be to buy a
[Thelio Massive](https://system76.com/cart/configure/thelio-massive-b1) as those
seem to be the coolest computers I've seen in a long while. Alas, I do not, and
I would like to make use of the parts I've already purchased before they are
completely obsolete, so being already well down the BYO System road I figured
it would be better to just finish what I had already started. Next time, though,
perhaps when this system starts to show its age, or perhaps when I make Director
at Google, should that hallowed day ever arrive. Or maybe when I'm done paying
off my car I can start payments on a computer that, configured the way I want
it, costs about us much as a midrange automobile.

This was the first build of parts I ordered from Amazon instead of NewEgg. While
I think the more structured search format of NewEgg still has some usability
advantages over Amazon the important thing here, and the lesson learned from
last time, is that server-class motherboards are a lot less tolerant of amateur
system builder screwups than their consumer counterparts. I can search on Amazon
for specific memory part numbers as recommended by the motherboard manufacturer
and come up with results, some of which are even eligible for Prime shipping.

I also learned not to try and get a server-class dual-CPU motherboard but to
look for one specifically targeted to Workstation builds. These types of
motherboards have a lot more of the consumer-friendly stuff that I normally
rely on in system builds, like NVMe M.2 controllers and SLI compatibility with
Nvidia video cards. There was no getting away from the SSI EEB motherboard form
factor for dual CPU setups but at least I was able to find a few chassis setups
that could accommodate the larger motherboard.

With Hilary gone for a chunk of the day at work, and me not having the energy
really to do much, it seemed a good day to take a stab at putting the new/old
parts together into a usable system.

Knocking on wood, the build went smoother than expected, and after installing
the old power supply, CPUs, and storage into the new chassis, motherboard,
and RAM, I was able to boot to the Gentoo LiveCD with no significant trouble.

I was super glad I had learned from the last system build how long to expect a
workstation-class motherboard with ECC RAM to take to boot. This is not your
typical PC boot sequence. Expect almost *a minute* of silent cogitation on the
part of the BIOS before any life signs, particularly on first boot as the system
has to figure out what parts are plugged in to it. Not the most comfortable of
minutes, I say, with multiple thousands of dollars of hardware quietly not
specifying in any particular detail if they are viable or not.

The Gentoo build went OK, I tried for a UEFI install first and then realized
that the BIOS was really going to prefer a legacy boot option, so changed the
boot partition back to ext2, rebuilt grub, and was able to boot in to a stable
system. I was very glad to note that I wasn't getting kernel panics or warnings
in the `dmeg` about memory fault errors every few minutes, so already this
build is big improvement over the last build I did.

Next project was to start the lengthy KDE/Plasma setup. While tackling that I
was able to spend a bit of time moving the network clock code for
{% include tag_link.html tag="sclork" %} into its own Quark and start writing
documentation for the classes involved.

There's only a few days left before I meet Bruno on Tuesday to drop the software
off for use in the first few weeks of the SCLOrk class. It's not enough time
to make everything as bulletproof as I would like, but I'm hoping there will be
enough in place that Bruno can kick out a couple of class rehearsals without
any major technical difficulties. "Hope is not a strategy," they say, but I'll
be keeping my fingers cross anyway.

