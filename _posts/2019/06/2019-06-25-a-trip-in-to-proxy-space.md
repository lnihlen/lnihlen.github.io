---
layout: post
title: "A Trip In To Proxy Space"
date: 2019-06-25
tags: [ personal, supercollider ]
---

A typical busy workday, punctuated by a commute on the Zero electric motorcycle, which keeps things interesting on that
trip to and from work. Then home for delivery from Saturn with Hilary, followed by exhaustedly watching an episode of
Worst Cooks in America on Hulu on the couch.

But I am literally feeling *stressed out* right now about how much I feel like I have to learn about the audio
generation parts of {% include tag_link.html tag="supercollider" %} and so it was off the couch and in to the office to
try and figure out some more about some of the live coding capabilities in SC.

Tonight it was about the ```ProxySpace``` and associated, diverse parts of ```JITLib```. The documentation is.. terse..
so I'm struggling to find usable examples or other useful milestones that might illuminate some of the meaning and real
power of the concepts being illuminated. I'm figuring out little pieces, like tonight I figured out some of the
notation, in that there's a connection between the environment variables as specified with the tilde ```~```` and the
current pushed ```ProxySpace````, and some other things like attaching a ```TempoClock``` to the current space or to
individual proxies within that space as needed.

So I started in working on a simple composition put together in real time, starting with a bass line. It's obvious how
to use Proxies to define either Patterns or Synth instances for playback with nice automatic crossfading between old
definition and new. The documentation also has elegant examples of chaining synth proxies together, or using the output
of a synth node to drive certain variables in a pattern, which seems exotic. But I feel like I'm missing some of the
obvious stuff (which is an experience I remember as common when learning SuperCollider concepts), like how to mix
environment variables into Proxies to allow for interesting things like changing the ```\instrument``` parameter in a
pattern, therefore allowing for realtime tweaking of synth objects while they are being performed, or even something
simpler like being able to have a common variable across different patterns that I can then tweak in a single place, for
example when doing something like modulation, being able to set the ```\root``` key in a bunch of ```Pdef``` statements
at the same time.

I'm sure that it's something obvious, and in fact I bet I have learned this before but didn't internalize it as the
important piece of information I would need *several months later* once I had figured out a bunch of other stuff about
SuperCollider. And again that continuing feeling of needing to know so much more about this program than what I have
learned, or anticipate having time to learn in the forseeable future. "Best effort" will continue to have to suffice,
but it feels damn well insufficient.

