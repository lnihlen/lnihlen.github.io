---
layout: post
title: "CIEDE 2000 Working"
date: 2018-11-10
tags: [ vcsmc ]
---

Had a chance this morning to do a binary search on the Halide CIEDE 2000 code
using the
[Wu, Bilal, Sharma Test Data](https://pdfs.semanticscholar.org/969b/c38ea067dd22a47a44bcb59c23807037c8d8.pdf), which conveniently includes data for intermediate variables for the
computation. After a lot of transcription of test data I discovered that my lazy
use of `pow(x, 2.0)` instead of just typing out `x * x` was producing bad
values. The multiplication is an optimization generally, but it was a bit of
a bummer to discover that kind of bug in `pow()`.

I started looking in to accelerating the
[SSIM](https://en.wikipedia.org/wiki/Structural_similarity) code with Halide
next. I found a pretty cool
[reference implementation](http://qpsnr.youlink.org/) that uses
[libavcodec](https://github.com/FFmpeg/FFmpeg/tree/master/libavcodec) to decode
and extract the video frames directly and compute the error metric, without
extracting intermediate files to images.

It's probably a huge distraction but now I'm thinking about how cool it would
be to bring in `libavcodec` to my own project, to allow me to pull the frames,
audio data, and metadata in one fell swoop. Will have to think about that,
although it's adding substantial time to completion of this revision.

