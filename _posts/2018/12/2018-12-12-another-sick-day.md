---
layout: post
title: "Another Sick Day"
date: 2018-12-12
tags: [ personal ]
---

The cold came back with a vengeance after minimal sleep last night so I had to
call in sick to work again today. I was able to keep an eye on some email issues
but generally stayed close to bed and the couch. I did manage this evening to
work up enough energy to do some more hacking on the
{% include tag_link.html tag="sclork" %} network clock.

I've been looking a lot at the source code for the `TempoClock`, as well as the
`Scheduler`, and tinkering with implementing my own `Clock` subclass, with
methods similar to `TempoClock`, that follow the timing specified by a remote
process. One thing I've learned is that keeping the system times in sync between
computers across the net isn't particularly useful, because the times that the
`Clock` objects in SuperCollider all rely on are actually `Thread` times, which
seed from the *process wall clock time*. So in fact even two different instances
of `sclang` running on the same machine may not have `Clock` time values with
any relationship to each other.

Building my own scheduler inside of my own `Clock` object is fun, and I'll be
working to figure out how to cleanly incorporate the diff signal from the
network clock following code which now seems to be working well. There's also
the tricky matter of the fact that normal `TempoClock` objects start with a
beat count of 0, and a network `Clock` object is likely to be following a remote
`Clock` that's already running and so has a much higher beat count than 0.

*One working day left.*

