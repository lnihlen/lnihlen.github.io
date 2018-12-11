---
layout: post
title: "Back to Work"
date: 2018-12-10
tags: [ personal, sclork ]
---

Again I had a lot of trouble falling asleep last night but I was finally able
to grab a few winks before getting up early today. This being my last working
week of the year there were just too many responsibilities calling to me in
the office for another sick day or even really one of working from home, so
I was up before dawn to commute in.

Long work day then home for dinner. I wrote a few more lines of code for the
synchronized time base, now computing a diff on the server and sending it back
to the client, which computes a round-trip time and stores the diff. It will
just keep a weighted rolling average of both of those metrics, and then use the
updated averages to supply a diff of the client system time from the server
system time, including network latency.

Having a synchronized clock inside of SC should hopefully allow for an
adjustable `Clock` object, which will do its own scheduling using the diff
supplied by the time base client. I could see these coming in two flavors,
including one that is remotely controlled by a network. The control API could
either be from an object or a `ProxyClock`, which drives the API by passing on
whatever functions are called on it.

I see these features as being separate, meaning that the client synchronized
clock looks like any other clock, it just takes a supplied `ClientTimeBase`
object, and the remote control can work with any supplied clock.

Mostly recovered by still have a sore throat and feeling super run down, so
that's probably all for tonight. But it feels good to make even minute
incremental progress.

