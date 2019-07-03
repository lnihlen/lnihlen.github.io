---
layout: post
title: "A Long Way Towards Sound"
date: 2019-07-02
tags: [ personal, supercollider ]
---

Longer day at work followed by an exploration with Hilary at a Dim Sum restaurant so it was only rather late that I got
home and had any time to work on the integrator code I've been building for my first
{% include tag_link.html tag="supercollider" %} UGen. There's been some interest in it on the ```#dsp``` channel on
the SuperCollider Slack, so I hope I'm not overselling it! I think the observation that mathematically "sound" doesn't
automatically equate to "sounds good" is a fair one. I also wonder if my esteemed colleagues whose implementations of
chaotic oscillators that I've been studying, that ultimately settled on a linear approximation, had higher-order
integrators implemented that didn't sound any better and so thought "why waste the compute?"

It was questions like these that kept me awake long past a reasonable bedtime last night, but it's been a long time (too
long, really) since I've felt that kind of creative flow and even trying to get down in to bed at a (late) hour was an
ill-fated thing when I'm feeling that much creative juice.

I was able to finish the rough coding for the integrator tonight, including typing out the other half of the constants.
Now it is time to start digging in to a terse implementation of a CMake build system for my own
[egSC](https://github.com/lnihlen/egSC) Quark, where I am planning on putting this and any other UGens that I ultimately
make. Given the fun I'm having with this one, I have a feeling I'm going to be doing a bunch more of these, and in
discussion with various SuperCollider senior developers it seems like
[sc3-plugins](https://github.com/supercollider/sc3-plugins) isn't the most future-proof of locations to drop this puppy
off in.

Of course, since I'm now mostly working on MacOS, there are additional complications for building and installing the
plugins, and I'm not sure if I'll even really bother with the support for the other operating systems for the moment.
But before I could even begin an attempt at compilation it was time to try and wind it down again for the evening.

I did decide on a test plan for today, I'll be licensing a copy of MATLAB and comparing the results of their ODE solvers
to mine, on a variety of different test functions (including the Duffing equation). It's been a long time coming to get
a copy of MATLAB, including back in the {% include tag_link.html tag="vcsmc" %} days, so that's also exciting, too!

