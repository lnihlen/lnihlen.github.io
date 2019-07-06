---
layout: post
title: "Finding Black"
date: 2019-07-05
tags: [ personal, supercollider ]
---

Holiday day today so I had more chance than normal to work on that Duffing oscillator for
{% include tag_link.html tag="supercollider" %}. First was debugging the fancy numeric integrator I had written for
second-order nonlinear differential equations like Duffing. I ran a simulation of another differential equation
provided in the help text, and modulo a few typos in constants, and switching the order of the inputs in MATLAB, I
was proud to have my code estimating the MATLAB results within 1% error.

That exhausted most of my free time for the day but I thought I would try and tackle actually getting some sound out of
the oscillator. Unfortunately I don't seem to be able to coerce much out of it. I can set the amplitude of the driving
sine wave to a really high value and get some small signal out of the Duffing oscillator code but it is clearly just
the input sine wave with a low-frequency DC component added on.

I am reminded of early days in graphics programming, where one spends a great deal of time looking at black screens,
until finally some pixels light up. It's just a matter of patience and re-checking one's work for like the millionth
time.

But now it is at an hour where if I did get any sound out I would probably disrupt the household, so further progress
will have to wait.

