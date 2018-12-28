---
layout: post
title: "SCLOrkChat Documentation Ready"
date: 2018-12-27
tags: [ personal, sclork ]
---

So yeah there's a reason why I set up that desk in the Living Room. Today I
learned that having a puppy really does mean that sitting quietly in my office
and working for hours on end is not a viable option. So it was a very halting
day for progress, with first trying to secure the dogs in the way that we do
when we're away, but they could hear me and weren't having the confinement.

Molly put up a huge fit, fussing and barking, so I let them out. Of course
they were not content to just sit on the couch either, so every 3-5 minutes
I had to get up from the office chair and go find out what Molly was attempting
to destroy. I tried tiring her out with several rounds of tug-of-war and fetch
but that bought me only a few minutes time.

All that aside I was still able to wrap up the first release revision of the
[SCLOrkChat Quark](https://github.com/lnihlen/SCLOrkChat), including reference
documentation on the client/server protocol, all classes, and an overall user
guide on how use the UI.

It's all definitely feeling a bit rushed but thin coverage still counts as
coverage. If I'm worried about anything it's that I haven't taken the time
to harden server or client from invalid messages. Also, all of the client-server
communication is happening via UDP. So there's some possibility of course that
packet droppage will create havok in my carefully designed server plans.

I've been thinking of building, either in SuperCollider as a Quark or perhaps
as a patch to the language, some support for a reliable UDP-based communication
protocol. If in the language it could be a wrapper class that provides two-way
communication between two `NetAddr` endpoints. It would wrap OSC messages in
its own message with serial numbers for retransmission. If it was more low-level
it might be cool to think about introducing
[QUIC](https://en.wikipedia.org/wiki/QUIC) support to SuperCollider's language
support for OSC. I think it would be an abuse of the OSC protocol itself, so
not sure it's even a good idea, just thinking aloud here, if you will.

Hilary just shared the trailer for
[Us](https://en.wikipedia.org/wiki/Us_%282019_film%29):

<iframe width="560" height="315" src="https://www.youtube.com/embed/hNCmb-4oXJA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Looks super cool.

