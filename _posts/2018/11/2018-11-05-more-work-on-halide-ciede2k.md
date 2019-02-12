---
layout: post
title: "More work on Halide CIEDE 2000"
date: 2018-11-05
tags: [ vcsmc ]
---

Had some time this evening to go over the CIEDE 2000 Halide code I wrote out
over the weekend. Sharma, Wu, and Dalal wrote a
[great paper](http://www2.ece.rochester.edu/~gsharma/ciede2000/ciede2000noteCRNA.pdf)
with some test data, providing inputs, outputs, as well as some intermediate
values on a few key variables within the computation. The trick is to use
the intermediate values to perform a binary search on the code looking for
where the values start to differ. What I've learned so far is that there are
probably multiple bugs, I can detect at least one difference in the early
part of the code, but it doesn't seem like a significant enough bug to account
for the large number of values at the end that are wrong.

It's slow and tedious work but at least feels like I'm making progress.
I'm suspicious that it may have something to do with the `select` statements
in the Halide code, I don't think the assumption that the logic tests are
being supplied sequentially holds.

