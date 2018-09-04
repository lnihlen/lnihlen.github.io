---
layout: post
title: "Unit Testing on Hobby Projects"
date: 2018-09-03
tags: [ vcsmc, i_made_a_thing ]
---

Today's
[commit](https://github.com/lnihlen/vcsmc/commit/d11a3e26edd722baa46a76aed06a2aa4ed5410c7)
adds unit test coverage for `State::Sequence()`. It's always a bit boring
unit tests for me, although I have found that designing code to be easier to
test has been a great way to improve the design of my code. Designing for
testability encourages a lot of other good practices; object tend to be loosely
coupled, with clear contracts between them, methods avoid side effects, etc.

But it's still boring to crank out unit tests for my own code, sometimes. So
why would I do that on a hobby project, which is supposedly just for fun? In
the years I've been working on vcsmc I've learned the hard way that a little
tedium in writing unit tests has gone a long way towards raising overall fun
on the project.

Some of the code in vcsmc, particularly around simulation and program generation,
can get pretty complicated. On top of that, evolutionary programming is
essentially a [fuzzing test](https://en.wikipedia.org/wiki/Fuzzing) against the
simulation and generation code.

Furthermore, because the programs are randomly generated, debugging can be
tricky because there's no obvious intent to the code. Reproduction of issues can
also be tough unless great care is taken to preserve the random seed and not
change any of the generation code between iterations. Unit tests bring
confidence that the code is *correct as tested*, so while writing them can be
pretty tedious they help me to avoid a lot more even more tedious and
frustrating debugging on the other end, once the code is written.

Or, maybe whatever it is they put in the food at work has taken its toll.

In any event, sequencing of individual `Codon` elements is now implemented and
tested. I'm imagining another nontrivial `State` method, `State::Apply`, which
takes a provided `Snippet`, returned by `State::Sequence` and updates the
TIA, registers, and timing values internally, based on parsing the bytecode
supplied in the Snippet. Because we also want to be able to apply `Spec` objects
to `State` I have a suspicion that there will be three versions of `Apply`,
with both `Spec` and `Snippet` calling a raw `uint8` pointer to bytecode.

I've been thinking about rewriting the `Spec` object to use `Codons` instead of
raw bytecode. It will take a bit of work to look through the current frame spec
setup and try to understand if there's any programming in there that can't be
expressed in the form of `Codons`. But since `Codons` are supposed to represent
state changes to the TIA it might make sense to consider adding any additional
capabilities if needed. It complicates table generation, in that that means
there are `Codon`s now that can be made that shouldn't be part of frame program
generation (such as turning `VSYNC` on or off). But what it would enable is
that the `Spec` parts become part of register fitting.

The thing I'll be thinking about, during the drought of personal time otherwise
known as "the work week," is how to sequence an entire `Genome` object into a
valid frame program in a way that is testable. Generally, the `Genome`
sequencing algorithm is to iterate through the `Codons` in order, have the
current `State` generate a `Snippet` from the current one, then see if the
`Snippet` can be applied subject to the constraints of bank switching and `Spec`
timing.

I'm thinking of a `SequenceNext` method within `Genome` that takes a few
arguments; the current frame time in cycles, the desired `Codon`, the next
`Spec` on the list, and a pass-by-ref of the `vector<uint8>` that the `Genome`
is building the kernel bytecode from. This method could apply the bank
switching, timing, and `Codons`. Or, perhaps, a pass-by-reference of the
iterators to the `Codon` list (a simple array) along with the `Specs`, so that
both can be advanced as needed. This method still seems a bit bigger than
strictly necessary but could work for a series of tests.

So, to leave note to myself for subsequent work:

1. Add the `State::Apply` method and relevant tests.
2. Investigate if `Spec` can be refactored to use `Codon`s, repair dependent
  code, deprecate other parts.
3. Implement `Genome::SequenceNext` and relevant tests.
4. Implement `Genome::Sequence`, which should now simply call `SequenceNext` in
  a loop.
5. Work on the refactor to the scoring system.
6. Implement a new version of `gen.cu`, the frame generation program.

Be a while before we have results, but at least the road ahead is clear.

