---
layout: post
title: "More Mutant Year Zero"
date: 2019-04-21
tags: [ personal, scintillator ]
---

So I mostly spent the day today sitting on the couch playing more Mutant Year Zero: Road to Eden, this time on the
Xbox One. It plays well there, despite the non-gameplay screens (like inventory management) having a fairly lazy port
interface where you are literally dragging a mouse cursor around with the joysticks and "clicking" with buttons. It's
not the end of the world, although if I'm going to be playing this game as much as I play most XCOM-style games I'm
going to appreciate the quality-of-life additions that the XCOM console ports had, assigning frequent actions to
controller buttons.

After cooking dinner, Hilary reclaimed the TV, and I know I was saying that I was going to prioritize working on the
{% include tag_link.html tag="supercollider" %} style guide, but its perhaps unsurprising that trying to advance an
effort so encumbered with emotional baggage is unappealing at best. So, instead, I answered the call of
{% include tag_link.html tag="scintillator" %} development and started trying to advance the
[vertex buffer work](https://github.com/lnihlen/Scintillator/issues/16) on the C++ side. It was a bit of slow going to
re-cache all of the Vulkan C++ work I had done to date, but I've started in on the bones of a general-purpose Vulkan
Buffer class, which looks like it will be useful for representing all sorts of data transfer needs between CPU and GPU.

There's only a bit of time left before bed and I'm torn between continuing on that thread or going back and playing
some more MYZ, or maybe even starting up a new XCOM2 squad.

I guess that is one cool thing about hobby projects. They're hobbies, so if I don't feel like jamming on them I don't
have too. On the other hand, the mountain of work behind even the first slice through Scintillator is not getting any
smaller.

