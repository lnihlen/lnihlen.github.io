---
layout: post
title: "Back Home, Threading Building Blocks"
date: 2018-09-22
tags: [ personal, vcsmc ]
---

Got up early to catch a flight back to SJC. In combination with our trip to
Disneyland this was feeling like a long time away from home, and it's good to
be back.

On the flight back I mostly slept but spent a few moments thinking about the
re-implementation of the keyframe group Evolutionary Programming software for
{% include tag_link.html tag="vcsmc" %}. One of the key dependent libraries
I've relied on in the past is
[Threading Building Blocks](https://software.intel.com/en-us/intel-tbb/details).
I had been struggling building high-throughput multi-threaded data structures
and algorithms, and TBB helped me get through that, radically improving the
throughput of my old software and letting me focus on implementing the fun bits
while doing the hard parts of concurrent programming far better than I probably
could in any reasonable amount of time. In other words, it's been a great
choice for a library.

But revisiting the library I got worried it was a bit faded. The
[main site](https://www.threadingbuildingblocks.org/) looks like it hasn't been
updated in over a year. I was glad to notice, however, that the
[github repository](https://github.com/01org/tbb) published a new branch,
`tbb_2019`, under a month ago. And the
[commercial documentation](https://software.intel.com/en-us/tbb-documentation)
looks pretty fresh as well, indicating it was last updated about two weeks ago.

I'm taking a read through the
[Task-Based Programming](https://software.intel.com/en-us/node/506100) examples
and documentation. I like the line that says that task-based programming is
appropriate for situations where there aren't many blocking operations and
there are many more tasks than there are threads. Given that each `Genome`
for each image will result in many tasks, and that the program will have to
evaluate a few million `Genomes` per frame, I think it's *very* likely that
this scenario fits the task-based programming scenario.

I was also encouraged to notice some discussion of
[OpenCL](https://en.wikipedia.org/wiki/OpenCL) nodes for flow graph
computing, even though I won't be building a flow graph for `epfg`. It makes
sense that Intel would not support an Nvidia product like CUDA right out of the
box. With the old `gen` program I had been wondering how to build in the
CUDA-accelerated portions of the scoring.

So, definitely going to run with TBB for this iteration. Not so sure about
CUDA, the last attempt at acceleration was probably a *pessimization* (hah!),
but with caching in place around the scoring, and the CPUs fully saturated with
tasks fitting multiple images at once, perhaps we can see an increase in
throughput by offloading the scoring work to the GPU. I think the first plan
will be to go pure CPU, then maybe look at bringing in GPU acceleration
down the road.

Next time I'll discuss a TBB task-based design for the main evolutionary
programming multi-frame approach, a program I am calling `epfg`, or
*e*volutionary *p*rogramming across a *f*rame *g*roup.
