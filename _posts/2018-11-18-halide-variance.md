---
layout: post
title: "Halide Variance"
date: 2018-11-18
tags: [ vcsmc ]
---

Had some time today to implement the Variance part of the SSIM algorithm in
Halide. First I had been hopeful that I could somehow do the same trick you
can do with Gaussian blurs, which is essentially a convolution with the Gaussian
kernel, but you can skip doing all elements in the 2D kernel by pre-computing
the blur in one direction, and then computing the blur across the other
direction using the blurred values.

First thing I had to adjust was to drop the padding around the input to the
Mean function, because I can't figure out a great way to not compute the
variance over the padding within the mean. Fortunately the Halide documentation
assures me that the `BoundaryConditions` doesn't cost too much of a performance
hit. I still have yet to refactor the unit tests to drop the padding but I'm
already re-thinking the design of the scoring system inside of the main app,
and liking how it's probably a lot simpler without the padding concern.

Next learning about the `RDom` functionality, which can serve as the Halide
flavor of a `for` loop, and also answering the question of how I'm going to
compute the final sums for the computation of mean scores.

I would say that I've hit some kind tipping point with Halide, but this not
being the first time I've learned a new library I'm sure there's going to be
at least a few more times in which I'm Googling around and cursing my confusion
and ignorance about Halide. But I do observe a few positive signs, such as that
the documentation no longer seems inadequate, but rather is the minimum required
to get someone productive without wasting their time.

Will still have to write some unit tests to cover the variance function, and a
lot of cleanup, but that's for another day.

