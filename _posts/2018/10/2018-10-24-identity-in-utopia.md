---
layout: post
title: "Identity in Utopia"
date: 2018-10-24
tags: [ sclork ]
---

Made an hour of time tonight to work some more on the SCLOrk stuff, mostly
focusing on the chat window now because the fanless server is working to meet
my needs, at least for the next rehearsal.

I dug in more to the `Registrar`/`Registrant` system this evening. It seems that
the system still has a chicken/egg paradox in that you cannot make a `Registrant`
to get access to the shared address book without first providing a `Peer` that
may or may not have a unique name.

I recognize that I'm getting pretty hung up on the unique names bit. At least
with this client/server architecture the system doesn't tightloop trying to
add a duplicate name. But when trying to develop the rest of the chat window logic
I keep getting hung up on funny bugs, likely caused by duplicate names. I'd like
to be able to open multiple chat clients, even on a single host, both for
purposes of development and general program robustness. And I do think there's
value in the chat app being able to automatically determine names for
individuals rather than just generic sign-in names on the individual laptops.

So I'm working on an OSC endpoint that can issue unique names for clients
based on their IP address and/or whatever name they are providing. I think I
can use `dnsmasq` on the server to control IP address, then I can build a
map from address to username, because we consistently use the same laptop from
session to session in SCLOrk rehearsals. The system will also keep a list of
names that it has already issued, so it can append numbers to the end of each
name in order to keep them unique.

There's lots of race condition kind of stuff here, where we could be issuing a
name on one thread, thinking it's unique, and then have another client be asking
for the same unique name and be issued that. Turns out, robust distributed unique
naming on a computer network is hard! (Who'da thunk?!). I don't think I need
a bulletproof SLA, I just want some kind of "try before you buy" model when it
comes to name assignment on the Utopia Peer group.

It also seems there's no easy way to make an RPC with a return value using OSC
primitives in sclang. I think at minimum I'm going to have to provide a path
back for the server, likely an IP address, port, and OSC endpoint to return the
unique name assigned to that request.

For first pass I don't think I'm even going to bother to try and synchronize the
set of unique names I'm keeping around for the naming service with the set
of clients in the `Registrar AddrBook`. I might add a simple one-way endpoint
to allow the clients to relinquish names, or I may just add both a serial number
and a server timestamp to each name, to help try and ensure uniqueness.

Ok, gosh, thinking about it, if I add a hash of the `date` salted with a few
bytes from `/dev/random` that might just be enough to keep a reasonably unique
name, and clients rendering that name can simply parse out the salt at the end
of the name when rendering it. No need for fancy theatrics.

Hopefully, writing out this blog and thinking about it saves me time over going
down the rabbit hole of implementing a server-driven version of this.

On to tomorrow.
