---
layout: post
title: "Some Thoughts on Scoring for vcsmc"
date: 2018-09-20
tags: [ personal, vcsmc ]
---

Another day-and-night-long meeting day in the Chicago office. Daydreaming about
{% include tag_link.html tag="vcsmc" %}. During a short break it occurred to
me that I could separate out the `bytecode` member variable of the `Genome` to
its own object, and then perhaps simulate/evolve against a whole bunch of
common frames at once.

On the old version of `gen.cu` I had built a feature that would allow a new
generation of kernels, for a new input frame, to be seeded from a single
input kernel, presumably from the prior frame in the same keyframe group. It
seemed like a good optimization to skip the early totally random noisy phases
of the new frame generation and get to the stuff that might be relevant for a
frame target image similar to the one we are now fitting against. The python
script could then break the movie into groups of images between keyframes,
which are assumed to be similar, and then seed each subsequent image in the
keyframe group with the fit from the prior image.

I never finished this feature, mostly because I got distracted by trying to
implement [SSIM](https://en.wikipedia.org/wiki/Structural_similarity), and
then hardware accelerate it, but also because I had some concerns about this
approach, namely:

  * The Evolutionary Programming algorithm rapidly converges on a pretty crappy
    solution, and then spends the lion's share of the time incrementally
    improving that solution, but the new target image is a bit different than
    the old target image, so I wasn't confident that the seeding kernel would
    save much time from just starting from scratch, or worse:
  * The algorithm may be stuck in a local minimum, and so we are propagating
    the shortsightedness forward, or conversely:
  * Slightly changing the fitness function (by slightly changing the target
    image) can be a great way to get an optimization algorithm out of a local
    minimum, so there could be an obvious visual *increase* in quality across
    the keyframe, as the fit gets better and better having subsequent
    generations of algorithms undergo changes in the fitness.
  * The "later frames look better" problem, which to be fair I never witnessed
    because of the SSIM distraction, I thought might be able to tackle by
    another pass through the keyframe group, perhaps multiple times,
    until some secondary quality improvement criteria had been met, or (more
    likely) the system detected it wasn't getting measurable improvement from
    revisiting old frames above some epsilon parameter. But in this situation
    the seeding becomes a further modification to the evolutionary algorithm to
    increase quality, and would likely represent a *de-optimization*,
    (sometimes delightfully called a *pessimization*) of the algorithm.

One other observation I had rattling around in my skull is that with the move
of scoring to the GPU, but the rest of the general Evolutionary Programming flow
living on the CPU, GPU utilization remains somewhat low. But I couldn't think
of a way to break the algorithm up so that both CPU and GPU remain saturated,
without perhaps processing multiple generations of the same time.

Since I've been refactoring stuff and re-thinking through parts of the code
I've been wondering if I should change up the approach to EP, or maybe change
to a different algorithm. So it occurred to me that one way I could increase
the parallelism of the system, while exploiting the objective shift to break
stagnation trick, and address the concerns around later frames looking better,
would be to process *all the frames in a keyframe group at the same time*.

The general idea would be that the system would create a unique thread for each
frame in question, and would maintain their own population of `Genomes`, but
allowing for sharing of `Genomes` across populations. Each thread will
translate the new `Genomes` in its individual pool and submit the resulting
kernels for scoring, with each kernel in every thread scored against every
target image in the keyframe group.

I have an idea for a scoring system that decomposes simulation and target
images into 32x32 pixel blocks, computes a hash fingerprint for each block,
and saves the score into a distributed hash table. I'm optimistic the caching
will really help to speed up score computation, because with single-point or
only a few mutations per generation most images change very little, and most
changes are localized to only a few pixels.

After scoring, the traditional Evolutionary Programming algorithm calls for a
tournament, which is where each individual from the population competes with
*n* random individuals, whichever individual has the better score gets a point.
Then the population is sorted based on total score and divided in to two
equally-sized groups. Each individual in the lower-score group is replaced by
a mutated copy of each individual in the higher-score group, and the higher
score group entire is copied in to the next generation.

Given audio changes the `SpecList` from frame to frame, even with identical
images each `Genome` will need to be Translated and then simulated for each
target frame. Then the per-frame simulated images can be scored, using the
above caching system. That means that each `Genome`, regardless of which frame
thread generated it, will end up with a score for each target frame in the
keygroup. The criteria for deleting a `Genome` is that no frame thread includes
it in its population.

A frame thread will begin the tournament as soon as every member of its
population has an assigned score. However, we expand the criteria of valid
participants in the tournament to *all genomes with a valid score for that
frame image*. This is how threads can share `Genome` objects across individual
populations, in that one generated by another thread could do well enough in
the tournament for another thread that it will get sorted in to the winning
half of the population for that other thread. Bear in mind, tournaments are
always held for individual threads and on the basis of score against that
individual image.

Some keyframe groups can be *massive*, like a few hundred frames, limited only
by heuristics put in to place in the encoder to make the video easy to seek in
or stream, since it's much easier to restart a decoder quickly on a keyframe
than it is a on differential frame. But, in that case the frames are going to
be very similar to one another, if not identical, so there should be strong
re-use of `Genomes` across the keygroup, keeping convergence time low for the
overall set. But memory pressure will probably be a concern, so will need some
way to configure an upper limit to the number of frames in a keygroup processed
at once. One potential mitigating factor here is that there may be a low number
of unique `Genomes` per image, since the same `Genome` is likely to perform
well across a large number of identical target images.

Next post on vcsmc will zoom in some to simulation/scoring/tournament system.

