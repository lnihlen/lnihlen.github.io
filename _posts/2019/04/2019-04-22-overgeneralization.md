---
layout: post
title: "Overgeneralization"
date: 2019-04-22
tags: [ personal ]
---

Got some hard news today at work, a bit ahead of schedule, and it definitely felt like a punch in the gut. I am reminded
that sometimes one really can't choose the circumstances in their life, certainly can't choose all of them, but we can
choose how we respond. It stings, it's awful, and it's demoralizing. But I'm trying my best to fight the temptation to
construct some sort of story about how my employer overall values me, or what my possible long-term career prospects are
there. I think, the long view, the relationships I've built and the reputation I've tried to earn will serve me. My time
here has not been wasted, the lessons I've learned and the skills I've gained I think will serve me wherever I go. But
damn, that still stings. No getting around it.

In slightly better news, the network card I ordered on Saturday arrived and I was able to throw it in to the workstation
and get it going, meaning that I'm happy hacking away on the high(er) horsepower machine, so yay! It took a few stabs
at restarting various parts of the network services but I'm back to the same network configuration I had with the
onboard Ethernet ports. And the workstation is now plugged in to a power conditioner and battery backup, so hopefully
the next time someone drives a car into the power pole down at the bottom of the street the workstation will have
enough time to start a graceful shutdown process. Although, to be honest, I'm not entirely sure what the root cause
of the port failure was on this system. It's a bit disturbing, particularly because I built this workstation with a
server-quality motherboard and nice beefy power supply.

I keep thinking it's a software issue because the NIC comes up and seems to be just fine, link lights ablinkin' and all,
and then I try and negotiate an IP address and get nothing back. Very odd. And frankly not worth my time bothering about,
at least until some other part on this motherboard fails. At which point I'm strongly tempted to pick up one of those
Thelio Massives from System76, because an American-made open source high performance workstation in maple trim is just
way too cool to pass up. Of course, to build a really powerful computer with System76 will set one back about $20K, so
maybe that's the reason I just bought a new network card for my existing workstation. But a geek can dream, can't he?
Maybe one day, if I ever do land that promo, I can contemplate buying a computer that costs more than a new economy car
or a luxury motorcycle.

In the meantime I should set about maybe working some more on writing code that could actually stress a massive chunk
of compute iron like that. It's been far too long since I had any time to mess about with
{% include tag_link.html tag="vcsmc" %}, which is the most horsepower-intensive thing I've written to date. There's also
the whole situation with {% include tag_link.html tag="scintillator" %}. I read today about a project to bring Vulkan
software rendering to Mesa, and saw some life signs in the project. I guess it started out as a Google Summer of Code
project in 2017, then went dark while the author went back to school, but has been picking up some steam again recently.

Having a software renderer, particularly with an LLVM backend for the shaders, could mean that I could write an
integration test suite for Scintillator, which could be very reusable as a non-real-time software-only backend as well.
It would likely start life as a different build configuration for Scintillator, which actually would represent a
different build configuration for glfw, which is currently the library I'm using to handle the platform abstraction
of including and linking Vulkan. I've added it to the (long) list of feature ideas for Scintillator, which actually
reminds me to create GitHub issues for these ideas, as I've been trying to use that as a centralized list for feature
requests and some very loose planning.

So life goes on, really, and perhaps work not having higher expectations of my performance means I'll still have some
very limited time to work on the various external projects that excite me so, when I'm not pouting on the couch eating
french fries and playing Xbox. Silver lining, or something like it.

