---
layout: post
title: "The Opacity of Halide"
date: 2018-10-06
tags: [ vcsmc ]
---

I've been feeling that [Halide](https://halide-lang.org) is a bit of a brick
wall. I've looked through the examples, tutorials, and even listened to the
introductory lecture by one of the principle authors on YouTube:

<iframe width="560" height="315" src="https://www.youtube.com/embed/WvzlaRpmtVk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

The language can be thought of in two halves, the first being specification of
algorithms and building a pipeline, and then the second is the scheduling of
those algorithms. That's the whole value proposition of Halide, which I think
is pretty smart. But I think that the developers of Halide have worked in it
for long enough that certain things that are obvious to them are nonobvious
to me, and so are taking a long time to figure out.

I chose one of the simpler tasks to try to tackle with Halide first, which is
the conversion of RGB to CIEDE Lab color spaces, a pre-requisite for the
CIEDE 2K color distancing algorithm I use for computing scores between images.

This conversion has a matrix multiply on the color components, in the conversion
from RBG to XYZ color. I use a D65 whitepoint. Halide seems to really shine
when reducing single (or possibly multi) channel images to single channel
output values. But a color-space conversion is a multi-to-multi channel
conversion, and furthermore each channel of output (L, a, or b) is a function
of *all three* input channels r, g, and b. Google and StackOverflow to the
rescue, in seems Halide can handle this capably with the `Tuple` concept.
The related tutorial is also quite useful, found after the fact. A multichannel
`Buffer` in Halide is thought of as a three-dimensional buffer, and is laid
out planar-style by default but can be trivially specified as the more familiar
(at least to this graphics programmer) interleaved style.

I also spent some time getting reacquatined with the python `colormath` library,
which I'm using to generate a series of test color conversions, for validation
of my Halide code. RGB to Lab conversion is not inner loop code, normally only
happening when the target images are first loaded, so I'm not going to spend
a ton of time optimizing this stuff. It was mainly to learn both how to express
an algorithm in Halide, to validate the library code, and to figure out how
I'm going to incorporate it into my build system and overall project workflow.

I finished the first draft of the `Generator` implementation of the conversion
code, and started in on the unit test, having generated the test input and
desired output, before needing a break.

Next time I'll spend some time wrestling with getting a `Generator` to actually
*do* something.
