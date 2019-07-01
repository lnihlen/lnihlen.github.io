---
layout: post
title: "The Missing Fehlberg Coefficients"
date: 2019-06-30
tags: [ personal, supercollider ]
---

The {% include tag_link.html tag="supercollider" %} developer meeting was this morning. They are productive discussions
about SuperCollider development, and it's good to have a chat with everyone on the line. They also are a pretty big time
sink for a weekend day, given my schedule, typically eating up 90+ minutes per call. After that call we took the dogs to
the beach, grabbed a late lunch, and before you know it my weekend day has pretty much vanished.

My goal for the day was to make some headway on an implementation of a reliable numerical method solution for the
[Duffing equation](https://en.wikipedia.org/wiki/Duffing_equation), a subject of some interest to me since having heard
Tom Mudd's album made using his own version of the oscillator. I am probably (definitely) over-engineering but in
designing my own solution I've been trying to get my head wrapped around the "Classical Seventh-, Sixth-, and Fifth-
order Runge-Kutta-Mystrom Formulas with Setpsize Control for General Second-Order Differential Equations" paper by
Erwin Fehlberg out of NASA in 1974.

The formulae are lengthy but definitely implementable, except it's not at all clear to me how to derive certain
important coefficients, here called ```c``` but in other more recent notation called ```b```. I'm driving myself a bit
nuts with this, to be honest, having re-read this paper now several times (just a start for a mathematics paper), with
no real enlightenment happening. There's a reference to this work in a more recent paper by Sharp and Fine (great
team name, too, for work in numerical methods) called "Some Nystrom pairs for the general second-order initial-value
problem", that gives the same numbers for the other sets of coefficients provided in the Fehlberg paper, which shows
that my understanding of the different notation is consistent, but seems to wave their hands at the providing of the
```c``` coefficients. It *does* however provide a full set of coefficients for a five-stage fifth-order solution
formula.

Five function evaluations per sample is probably a ton, and this whole approach is probably leaning way too hard towards
accuracy and way too far away from computational efficiency. But there's a whole class of oscillators depending on
general second-order differential equations and I'd like to be building something here that I know is somewhat
mathematically sound. Furthermore, it occurs to me that a step size can be computed from these numerical methods,
generally, so it may be possible to do an integration step that is larger than the timescale of a few samples and then
simply linearly interpolate between those two any samples that lie between. We'll have to see if I can work from this
paper, although I suspect there will be several more mysteries to uncover. One challenge is that these papers are old
enough that there is certainly no example implementation downloadable at a url in the paper, like you might find on
more modern papers. A peek at an implementation of these would certainly be enlightening.

Ah, actually thinking through the notation differences I notice that the higher-order function in the Fehlberg paper
gets the hat, and in the Sharp and Fine paper the lower-order function gets the hat! Basically in all these methods
a comparison is made between the next-highest precision version of the approximation and the current precision, and if
it exceeds an error bound then that is used as a signal to reduce the step size because there's too much error being
encountered at the current level of integration step and precision. Since that next-highest order precision can usually
be computed at a small incremental cost this meant that an understanding of approximation accuracy can also be gained.
But the newer Sharp and Fine paper suggests using this more accurate estimate as the finished product, and comparing it
to the less accurate one only for error estimation, which seems to me more sensible.

As always when reading these kinds of papers, enlightenment (if it comes at all) comes after hours of confusion for me.
And, of course, I have exhausted the available free time I had today in order to begin implementation, or to make any
music. But it was great fun to exercise a part of my brain that I haven't for a while, reading old-school mathematics
papers!

