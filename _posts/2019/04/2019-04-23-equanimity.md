---
layout: post
title: "Equanimity"
date: 2019-04-23
tags: [ personal, scintillator ]
---

It may be the fact that I have some kind of adventure vacation starting less than two weeks away, or it may be that I'm
demonstrating some hard-earned resiliency (or perhaps a bit of both), but despite the rather hard hit at work yesterday
I woke up this morning feeling pretty much normal, and had a pretty much normal day at work too. Perhaps it has been
the motorcycle rides in to work, with such beautiful weather the temptation is to ride every day, and I've been doing
just that. So lots of time for quiet reflection, and arriving at work feeling relatively chill, as I carve through
parked traffic on the 85.

There's more perf fallout at work, mostly in the form of letting folks on my team know the results of their own promo
attempts. Some good news, some bad. Then home and had a minute while Hilary was out and the dogs were still at doggie
day care to really dig in to some code on {% include tag_link.html tag="scintillator" %}, so did that. I think I'm
starting to grok how I want to use the vertex and index buffer example code on the
[Vulkan Tutorial](https://vulkan-tutorial.com/Vertex_buffers/Staging_buffer) to create some kind of general-purpose
host-to-device data transfer system. It's certainly overkill for the first iteration of the synth but it also represents
me starting to branch out and specialize more from the tutorial code, working instead from Vulkan API documentation and
other developer articles instead of just staying narrowly focused on the tutorials.

This kind of explicit memory management is one of the appeals of Vulkan, and developing a rich kind of API where the
arguments being passed into the vertex and fragment shaders can be specified at ScinthDef time, packed into a shared
buffer, and then efficiently transported to the card make for some pretty cool evening programming work. There's also
push constants to think about. So while I type through the tutorial some too, and think about how best to design the
sort of abstraction layer I'm trying to build around the Vulkan objects, I also go off and read about new concepts
in the API, read ahead in the tutorial, and stare off in to space some thinking about how I want it all to fit together.

I'm aware, too, of wanting to fit in some documentation in both design documents and better self-documentation in the
code. My experience with [Doxygen](http://www.doxygen.nl/) or other self-documentation tools has been very patchy,
however. A lot of projects seem to think that just having very minimal Doxygen coverage is enough to consider a project
"documented." I think that it's potentially a good start, but that often the Doxygen becomes just a slightly reduced
source of information compared to the actual source code, and so basically just a complete waste of time.

It looks like [Sphinx](http://www.sphinx-doc.org/en/master/index.html), in combination with
[breathe](https://github.com/michaeljones/breathe) can take Doxygen output and do interesting things with it. But note,
yes, it all goes back to Doxygen in the end for C++. So that's interesting. I guess part of the impetus to get some
documentation going here is that the SuperCollider side of the coding has all of the same sorts of facilities. The
help system built in to the IDE is great, and I have every intention of carefully documenting the SC API for
Scintillator. So why would I skip the C++ side?

I've fallen into another documentation hole here, reading through the Doxygen web page. Yeah I ain't mad at it. There's
plenty here that I think could help both keep the code self-documenting but also produce some expressive, useful
documentation in HTML for standalone consumption.

It's just more work, more drag on the system and a really *weird* way to have fun, writing documentation. But maybe
really it's not much different from this blog, and likely (at least hopefully) to be read by a few more people. No
judgement, right?

