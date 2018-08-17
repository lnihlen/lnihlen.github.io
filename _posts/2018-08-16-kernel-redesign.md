---
layout: post
title: "kernel redesign"
date: 2018-08-16
tags: [ vcsmc, i_made_a_thing ]
---

The kernel object within vcsmc is an abstraction around a randomly-generated
set of [6502 machine instructions](http://www.6502.org/tutorials/6502opcodes.html)
intended for execution on the Atari 2600 simulator or hardware. It will produce
an image which is then scored against the target image. That score is used to
decide if the kernel should be copied to the subsequent generation, with
possible modification.

In order to generate an image the VCS is responsible, each frame, for modulating
the scanning electron beam by turning it off and initiating the vertical refresh
at a specific time in the frame. Additionally we play back audio on the Atari
by manually setting voltage values on the speaker controller for a fashion of
extremely low-fi digital audio. Both the scanline and digital audio needs are
requirements on the timing of certain instructions being issued within the
frame.

The random kernel instructions consist of two classes of opcodes, immediate loads
and zero page stores. The immediate loads LDA, LDX, LDY load a hard-coded random
byte value from bytecode ROM into one of the three registers, A, X, or Y. These
are 2 bytes in size and take two CPU cycles to execute. The zero-page stores
STA, STX, STY store the current value in the specified register into one of the
subset of TIA memory-mapped registers existing in the first 256 bytes of address
space. Because the CPU doesn't have to load 2 bytes of address the zero page
stores take 3 cycles to execute.

I chose these two classes of instructions because they represent the fastest
way to change the state of the TIA, but this comes at the expense of frame
programs much larger than the ROM address space of the Atari. So additionally
we will need to be able to insert bank switching instructions, along with some
byte padding, to support bank switching.

In summary the kernel requirements are:

1. Randomly generate an entire frame, thought of as a fixed number of CPU cycles,
perhaps based on some initial random key.

2. Provide a pointer to the bytecode of that frame for simulation purposes.

3. Allow overriding of instructions in the frame program with supplier-provided
bytecode at either timing or size offsets within the existing program. This may
require repair of the underlying bytecode to keep the over-written bytecode
stream valid.

4. Allow for random mutations and efficient copies.

I'm inspired by the process of transcription from DNA to RNA to protein.
I envision a system where the DNA describes a system of *semantics*, essentially
a Domain-Specific Embedded Language. This I envision as a giant enumerated type
describing all potential state changes to the TIA render hardware, but in terms
of meaning instead of bit value in register, so for example something like
*set missile 0 size to 4 clocks* instead of opcodes to load a value into a
register and store it into the appropriate TIA address (NUSIZ0 in this case).

Kernel generation will create a lot of these DSEL commands, probably many more
than will be used in the final bytecode. There are a few special ones I can
envision, such as *wait XX cycles*.

To generate a kernel bytecode blob the Kernel DNA/DSEL will go through a
*transcription* process. We track the current state of the TIA and register
values, taking care to pack as many state transitions as is possible into the
output bytecode. So, for example, if the instruction is to *enable missile 0*
and the D1 bit is already set in ENAM0 the instruction will be ignored entirely.
Or, if the D1 bit is not set, then the transcription process will inspect the
three existing registers with pattern XXXXXX1X, meaning that all but D1 bits
are don't care, and see if any of the three registers match. Assuming register X
matched that pattern, then the only bytecode issued would be STX ENAM0.

Also during transcription we apply the hard-coded constraints, which are
specified for certain timings within the frame. If transcribing the next
command would take longer than available time before deadline a small delay
is inserted and then we defer transcription until after the constraint is
applied. This means we also insert the bank switching commands during the same
process.

Modification of the kernels can mean re-randomization of particular DSEL
instructions, re-arrangement of a few sections of instructions, or perhaps
a new kernel could be formed by merging two kernels section-by-section based
on a section-score weighted random selection.

This allows sections of instructions to be modified or moved resulting in
perhaps very different bytecode and timings but still the same behavior as
called for by the DSEL. Furthermore, changes are more likely to be meaningful
because redundant bytecode is never generated.

One last consideration is formerly  instruction generation had been based on
uniform random selection of a few branching choices - generate a load or store,
then which register or address, then which value. This naturally weighted the
distribution of possible instructions in an counterproductive way, weighting a
change in some of the more obscure registers like REFP0 equally to a change in
a more likely useful register the GRP0. By flattening the list we pick from
randomly to all possible state changes to the TIA we naturally distribute the
probability into areas more likely to result to interesting changes to the
output image.

I look forward to implementing this new kernel, now more appropriately named
a *genome*.
