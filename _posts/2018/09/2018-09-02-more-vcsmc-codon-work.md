---
layout: post
title: "More vcsmc codon work"
date: 2018-09-02
tags: [ vcsmc, i_made_a_thing ]
---

Watching the new (to us) season 8 of
[Great British Bake Off](https://en.wikipedia.org/wiki/The_Great_British_Bake_Off)
with the new hosts. Of all the people to not replace Paul Hollywood was likely
my least favorite choice. But I have to say, one episode in, it really works.

In any event, spent more time
[hacking](https://github.com/lnihlen/vcsmc/commit/1b2744b8d0b67c03c656f1102091525a33fb2c26)
on vcsmc on the living room desk. Worked on the bytecode sequencing process
inside of `State`. Some complexity emerging here for optimization:

1. `kWait` Codons require no state changes so can happen without introspection.
  There's no opcode that waits for only 1 cycle, so the shortest wait is 2
  cycles, and max is 255. The `NOP` instruction waits for 2 cycles, and I chose
  a `BIT` zero page opcode to wait for 3 cycles without changing any meaningful
  state.

2. All other Codons right now call for a state change in the TIA. Base case is
  that the target value is loaded into a register with one of `LDA`, `LDX`, or
  `LDY` immediate instructions, and then stored into the zero page TIA address
  with the corresponding `STA`, `STX`, `STY` opcodes. Two special cases exist:

    1. Some TIA address are *strobe* addresses, meaning they are write-only and
      don't key off the value being written but only the timing. These should
      not impact register fitting at all, because any register will do.

    2. For non-strobe TIA addresses, it's possible the desired state matches the
      current state, and so this codon serves as a no-op.

3. For some multi-purpose registers we need to get the current state of the
  register for the bits not being set by this Codon and mask it in to the
  target value, so those bits remained unchanged when the register is
  re-written with the updated value. Specifically these are `CTRLPF`,
  `NUSIZ0` and `NUSIZ1`.

4. Assuming we do need to make a state change register fitting happens in two
  stages:

    1. We track current state of the registers and then comparing the target
      value against each register (with don't care mask) to see if any of the
      current register values match that. If we can re-use a register value that
      saves us a load operation so we pick that register.

    2. Failing that we track last usage times of each of the three registers and
      pick the least recently used, in the hopes of maximizing value lifetimes
      in an individual register and driving the likelihood of re-use.

5. Issuing the store command is comparatively easy, as we've already identified
  the register with the target value, and that's the finished Snippet.

Got through *most* of this, before discovering some of the extra corner cases
around strobes and the early-out optimizing out a non-strobe Codon that doesn't
change state.
