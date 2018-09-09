---
layout: post
title: "More work on vcsmc"
date: 2018-09-01
tags: [ vcsmc, i_made_a_thing ]
---

### Kernel/Genome redesign progress

Finally grabbed some time to
[hack](https://github.com/lnihlen/vcsmc/commit/32cdea416193ee10706b50669aaa004891d09ed8)
on vcsmc. The refactor from treating the bytecode as the genetic code, to using
the codon transcription model, is feeling like it's going to take some time.

But it also feels like the right direction. Sometimes, when working on a
refactor, it can be a cool feeling when the new code flows a little more
easily than the old work did. It's nice to get a chance to rewrite the gnarly
part of the kernel bytecode generation. There are a couple of different
constraints that all need to be monitored at the same time:

* The timing constraints of the next specified thing that needs to happen in
  the frame program, such as turning on vertical blanking or audio sequencing.
* Bank switching requirements, as frame programs typically exceed the size of
  the 4K bank multiple times.

So the strategy of bytecode generation is to use a `State` object to keep
track of all TIA and register state, which allows conversion from a `Codon`
to efficient bytecode, re-using register values when possible.

For each `Codon`, until we've generated sufficient bytecodes to fill the
entire frame of time, we do the following:

1. Speculatively generate the bytecode for the next `Codon`, then determine
  the byte size of the generated bytecode as well as the timing. We will need
  to determine if this bytecode violates either the timing or bank size
  constraints.
2. It's tricky to consider situations where the size and timing constraints
  could be violated at the same time, because we may reach a situation where
  mitigation of one results in generation of alternative bytecode that causes
  violation of the other. Given that the timing constraints can't move I've
  decided to leave some room in the bank size requirements. We therefore first
  check to see if the next upcoming required instruction from the specification
  timing is happening sooner than the speculative bytecode would complete.
  * If so, we issue `NOP` opcodes until arriving at the specified timing, then
    issue the bytecode as specified by the spec, and go back to step 1.
3. We then check to see if the bytecode size has crossed over the limit of the
  size where we start to try to issue a bank switch `JMP` opcode. If that
  is the case we emit those bytecodes and then go back to step 1 again.

### VCSMC Bank Switching

The bank switching scheme is relatively straightforward compared to
[historic bank switching strategies](http://www.classic-games.com/atari2600/bankswitch.html).
This is because the Atari had no read/write line routed to the cartridge ROM,
so programmers had to be inventive when trying to signal to the ROM what bank
the program code has requested next.

Because we only ever advance forward in the frame program, and an individual
frame program consumes at least a few banks entirely, I devised a bank switching
strategy which signals bank advancement by jumping to the very top of the
program address space at `0xf000`. The last few bytes of the ROM address space
also contain two addresses, a jump table. One is for when the Atari is turned
on or reset, and the other is for a game mode change. We hard code both to
also jump to the start at `0xf000`.

Perhaps later I might want to respond differently to a reset or mode change.
In particular the mode change button could signal an advance to the next
video on the custom cartridge. But for now we just hop back to the start of
current bank.