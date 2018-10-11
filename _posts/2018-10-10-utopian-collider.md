---
layout: post
title: "Utopian Collider"
date: 2018-10-10
tags: [ supercollider ]
---

After some more fussing with Gentoo on a Pi, and realizing what an uphill climb
it is, I started in on the actual work involved with exploring the Supercollider
Utopia quark. Didn't get far, noticed that when two different computers sign in
with the same username, which is seeded from a `whoami` command line, the system
loops trying to reconnect.

Good to know. And that's as far as I got. I think a good experiment would be
to get the `BeaconClock` running with a synchronized tempo, then record the
audio output from the two devices, to measure time differences in the two
pulses. I'm curious to see how they vary over time, too.

Also reading online a bit about network
[clock synchronization](https://en.wikipedia.org/wiki/Clock_synchronization),
to see if we could build a more robust `BeaconClock`. But first we will
characterize the existing algorithm in Utopia, under ideal conditions (two
high-powered computers on GigE with ping times < 1ms), to see what kind of
audio delay issues we encounter.

Just realizing I need to load in the drums, or at least get them ready. Got an
{% include tag_link.html tag="oort_cloud" %} gig tomorrow night at the Caravan
Lounge in downtown San Jose.

