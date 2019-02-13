---
layout: post
title: "Thread Sharing of Genomes in vcsmc"
date: 2018-09-21
tags: [ personal, vcsmc ]
---

Last day in Chicago, rising early tomorrow to catch a ride to the airport and
then a flight back to the beautiful Bay, the South Bay specifically, landing in
SJC.

Been a long week and I'm totally fried. But I've been thinking some more about
the next layer of detail on the per-thread, per-image scoring system I outlined
in the post
[yesterday]({{ site.baseurl }}{% post_url /2018/09/2018-09-20-vcsmc-thoughts-on-scoring %}).

Since each thread is fitting against its own target image, and maintains its own
spec, this actually decouples all of the threads from one another for the
purposes of `Genome` generation, simulation, and scoring. This simplifies the
design of these elements because they do not need to be designed with efficient
multi-threaded usage scenarios in mind. In terms of sharing `Genomes` that
other threads generated they still need to be Translated with the `Spec` owned
by the recipient thread, so from that perspective their origin really has little
bearing on their design.

So far the individual thread algorithm looks largely the same as before:

  1. If first generation, fill the population array with randomly-generated
    `Genomes`. Otherwise skip to step 2.
  2. Any `Genome` in the population that does not have a Translation to a
    `Kernel` gets Traslated, then Simulated, then Scored.
  3. Conduct tournament across entire population, tally scores, then sort
    population by score highest to lowest. We now have a rough ranking of
    best-performing `Genomes` to worst. In order to build the population for
    the next generation I want to source some of the higher-performing `Genomes`
    from the other threads. But I want the threads to be able to run
    independently of one another. So:
  4. We submit references (likely by `std::shared_ptr`) to the top *third* of
    the population to a readers-writers concurrent storage system, where they
    are stored as the fittest individuals for this thread's most current
    generation. Each generation they are re-submitted and so any `Genome` that
    has fallen out of favor globally will eventually hit a reference count of
    0 and then be reclaimed. We call the top third the *elite cohort*.
  5. After submission to the global list the top third propagates to the next
    generation. The next third of the population is provided by the traditional
    Evolutionary Programming method of copying a top individual and then
    mutating. The final third of the population is provided by selecting
    at random `Genomes` from the elite cohorts of other threads.
  6. There's a possibility that some of the elite cohort `Genomes` from other
    threads may already exist in the working thread's population. If so, they
    are copied into this population and mutated. Thus `Genomes` that do well
    against multiple target instances receive additional attention from the
    algorithm. The thread can then restart at the top.

As far as termination conditions I don't think any thread should stop working
until all threads have reached some sort of termination condition. I'm hopeful
that if one thread has advanced further than others in terms of quality it will
be able to provide higher-quality individuals to the other frames for
evaluation, and perhaps after spending some time evolving against these other
criteria those individuals will actually break the advanced frame out of a
local minimum, thus continuing to raise the bar. We shall see how it works
in practice, however.

I've been wanting to invest a great deal more effort in to higher-quality
HTML-based verbose logging, including animated GIFs of evolution progression.
Since we're building stuff from scratch, think I'll give that some serious
thought up next.

