---
layout: post
title: "All the Interesting Sounds Were Bugs"
date: 2019-07-07
tags: [ personal, supercollider ]
---

Spent the morning traveling back home from our anniversary trip, which left me indisposed until the afternoon. This was
our first night away from the {% include tag_link.html tag="chickens" %} and while the person who looks after the house
was keeping an eye out for them I was glad to see them all present and accounted for, with consistent access to food and
water. We cleaned out their coop

This left a few hours in the evening to play around with the Duffing oscillator project for
{% include tag_link.html tag="supercollider" %}. It was nice to hear the oscillator on actual external speakers. It was
a good way to remove each individual bug from the UGen, unfortunately leaving me in a place where the Duffing oscillator
is now quite stable and computationally efficient and sounds completely boring. The weird sounds were of course all
coming from implementation bugs.

I made a start on ```DuffingExt```, which drives the duffing oscillator with a provided audio-rate signal instead of
relying on the internal oscillator. This was helpful to find the bugs in the ```DuffingOsc``` version, as it forced me
to clarify some of my thinking around time scale adjustment to keep the frequency response of the oscillator
comparatively flat. I'm doing the same trick for ```DuffingExt```, but of course now have to coordinate simulation time
with the sample rate of the driving signal. The goal is that if I use a ```SinOsc``` to drive the ```DuffingExt``` it
should sound identical to the ```DuffingOsc``` with the same driving frequency.

I completely threw out the Sharp and Fine fancy integrator I wrote because it was both computationally less efficient
and also less stable than simple linear integration. The time steps we are now integrating across I think just break
down the assumption of the underlying Taylor expansion built in to all of these RKNG integrators. At least it was fun
to write!

I'm heading in to surgery on Tuesday so there may be some down time on the blog. I'm collecting distractions to have
while away at the hospital. I'm hoping I'll have more time to work on the oscillator but with all the drugs and stuff I
might have to settle for less *demanding* ways to occupy my time, at least temporarily.

