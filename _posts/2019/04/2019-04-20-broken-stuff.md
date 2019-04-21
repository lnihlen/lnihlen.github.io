---
layout: post
title: "Broken Stuff"
date: 2019-04-20
tags: [ personal ]
---

I had really hoped to dig in top a solid day of work on {% include tag_link.html tag="scintillator" %}, maybe even make
some progress on the document I've been working on for the {% include tag_link.html tag="supercollider" %} style guide.
But no, fate conspired against me on these wishes. I had ordered a few cables and a new desk chair, so after sleeping in
Hilary and I headed in to Scotts Valley to pick up the chair.

When we got home I turned off the workstation and rerouted it with the longer cables, to give me some more leg room
under the desk. Than I turned the machine back on and, surprise surprise, the network interface won't come up. So there
was two or three hours gone trying different things. There was some circumstantial forum evidence that maybe it had
something to do with a buggy interaction with ACPI, so I recompiled the kernel without ACPI support enabled. Maybe I
should have taken the observation that half the kernel recompiled after disabling ACPI as a bad sign. Because, sure
enough, that new kernel didn't even boot.

Sometimes working on Gentoo is like that, you have a problem with part of the machine, and then suddenly you're booting
from the LiveCD and chrooting in to your actual environment. Or, in this case, booting a known good old kernel (which
also can't see the NIC). No dice. There's a $30 PCI-E NIC coming to me in the mail for Monday. I had noticed that those
onboard Ethernet ports were increasingly unreliable but I have to say I'm not thrilled with the idea of just installing
a separate card and calling it a day.

I multitasked and got Windows installed on an old Linux workstation that I've been meaning to turn in to a gaming rig.
At least that worked OK, and I got a little fix of Diablo 3 after getting that going. I found a new game too that's
pretty fun, Mutant: Road to Eden. Got a neat mix of XCOM and S.T.A.L.K.E.R. with some interesting Howard the Duck
mutant twist in there. Pretty fun.

So maybe tomorrow I'll get some time in on the personal projects? We'll have to see. Time is of the essence on that
document for SuperCollider, so think I'd better start there.

