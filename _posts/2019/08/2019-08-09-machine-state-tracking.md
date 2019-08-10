---
layout: post
title: "Machine State Tracking"
date: 2019-08-09
tags: [ personal ]
---

I had been working for some time on the "permanent" Asset system for {% include tag_link.html tag="sclork" %}, and then
recently turned my attention towards refactoring the chat system. The interesting observation from this morning,
however, is that not all information in a chat system is worth archiving, such as the current state of the machines
connected to the network. I'm pushing forward with some additional code to check current suitability of the client
laptops in a shared performance. Particularly during setup for a performance, often under time constraints and in an
unfamiliar environment, it's useful to know which machines are connected to the network, running the different parts of
the SuperCollider runtime environment, etc.

So it's still feeling like a bit of a diversion, but not a terrible one, to mix the machine state tracking into the chat
system. When all chat messages are associated with an author and added to a permanent record, the thing that is
ephemeral is the states of the individual connections and machines powering them. Because my hope is that folks will be
able to switch computers arbitrarily, machine state information really can be ephemeral. But we still do need to know
*who* is connected at any particular time. Hence, the current work. I'm hoping to wrap it up this weekend, at least in
simplest form. But I will have to fight the temptation of adding a bunch of fancy tracking to the system, like available
memory and CPU load.

