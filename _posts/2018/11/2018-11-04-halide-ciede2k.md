---
layout: post
title: "Halide on CIEDE 2000"
date: 2018-11-04
tags: [ vcsmc ]
---

So yeah, it was just a matter of hard work, defining a `Func` for each of the
intermediate variables in CIEDE 2000 to build up a
[big pipeline](https://github.com/lnihlen/vcsmc/blob/2ec7d67442ec277daef7656dc13ce67d806936e5/src/ciede_2k_generator.cc). I'm only passing a few of the test cases right now, and
it's not obvious to me looking at the inputs for those test cases which are
passing what the pattern might be.

I *did* learn the correct use of the Halide `select` statement, which really
functions more like a `case` statement than it does like the ternary operator
I had originally thought. It's a lot of math to be staring at so I'm going to
take a break from that problem for the evening and come back another day.

The goal is to deprecate all the CUDA code from the project, and replace it with
Halide. I have a dream of building a high-performance system and then optimizing
the Halide code to run on it, CPU and GPU.

After fixing the CIEDE 2000 code up, next up is the
[Structured Similarity Index](https://en.wikipedia.org/wiki/Structural_similarity)
measurement, which was traditionally the slowest part of the old `gen.cu`
pipeline.

