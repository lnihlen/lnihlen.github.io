---
layout: post
title: "Gutter Synthesis"
date: 2019-06-28
tags: [ personal, supercollider ]
---

There's a ```#dsp``` channel on the {% include tag_link.html tag="supercollider" %} Slack and one of the participants
shared a link to a [fascinating album](https://tommudd.bandcamp.com/releases) today by Tom Mudd, called "Gutter
Synthesis." It uses a chaotic oscillator called the [Duffing Oscillator](https://en.wikipedia.org/wiki/Duffing_equation)
which after work and some time decompression playing Feudal Alloy I took a few minutes to dig in to. It's a second
order differential equation with no closed form. I think I would like to try and implement it as my first attempt at
writing a SuperCollider UGen plugin.

Tom Mudd does supply an implementation of this oscillator but it is in Max/MSP and, given the creative output on his
album, this seems like an oscillator worth playing around a bit with in my native environment, as well as an excellent
intro in to chaotic oscillators in general. Turns out Nick Collins has implemented a very similar set of equations
already in his SLUGens set, called the [DoubleWell](http://doc.sccode.org/Classes/DoubleWell2.html) oscillator. It has
a similar differential equation setup with fewer parameters. Looking at
[the source code](https://github.com/supercollider/sc3-plugins/blob/master/source/SLUGens/SLUGens.cpp#L1373) it seems
Nick is using the Runge-Kutta method to obtain an iterative solution for those equations.

This lead me down two excellent rabbit holes, first finding the book Nonlinear Dynamics and Chaos, by Steven H.
Strogatz, followed by finding the [lecture slides](http://www.nodycosy.unich.it/files/velarde_oscillators.pdf) for
"A Brief History of Oscillators and Hair Styles of European Men." I want to implement all of these oscillators, which
are all described in the language of differential equations.

So there's going to be some work here on making some new UGens based on a variety of different oscillators, I think.

But of course none of this was making any audio, so as I was out of time I made a quick detour through finishing the
second practical in the Andy Farnell Designing Sound book. I now have dial, busy, and ring tones also running through
an implementation of a phone line filter. This was also a useful exercise in chaining ```Ndef``` expressions together.

So the evening wasn't a complete waste for that. But honestly it's hard to feel really bad about getting lost reading
documentation right now. I remember when I started working on Chrome at work, there was a period at the beginning where
I just read source code for probably a month. Didn't write hardly anything, just poking around in different directories,
trying occasionally to get things to compile (I was porting it to the PlayStation 3, a big-endian machine). I started to
get really freaked out that I wasn't writing any code, but what I realized was that I had internalized a great deal
about how Chrome was put together, including the parts I would need and the parts that I would need to work to exclude.

There's a balance to be struck here between "trusting my creative instincts" and "allowing myself to go with what is
comfortable," that is sinking back in to the habit of not making any audio with SuperCollider but just builing
infrastructure. Perhaps in the end it is about trying to honor the calling I feel. But I think chaotic oscillators seems
like an interesting avenue of exploration for making sounds that are more organic-feeling and rich coming from a
computer. There is also the whole music theory backlog of literature I am queuing up for myself but that does feel like
a distraction to a certain extent, in that I'm not particularly interested in making traditional music.

As a general rule any forward progress is acceptable progress. And I want to continue to try and make some sounds come
out of SuperCollider every single day. Even if only for a few minutes at a time.

