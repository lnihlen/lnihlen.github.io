---
layout: post
title: "Anniversary"
date: 2019-07-06
tags: [ personal, supercollider ]
---

Today is my 6th wedding anniversary with Hilary, so to celebrate we traveled down to Monterey for a day at aquarium,
followed by dinner at a lovely sushi restaurant in Carmel. Six years and still going strong! I'm proud of us and happy
to still be married to Hilary.

There was also time to work on my Duffing oscillator for {% include tag_link.html tag="supercollider" %}. The discovery
today was the formula on the Wikipedia page for steady-state amplitude of the oscillator as a function of all other
parameters. It turns out that in order to get constant amplitude of +/-0.5 there's a *six orders of magnitude*
difference in gain required in input signal, from around 10 at 20 Hz to around 1 million at 20 kHz! This means that the
current Duffing oscillator is also acting as a low-pass filter with 60 dB rolloff across audio frequencies.

If I was just thinking about the oscillator I'd be OK with what I'm doing right now, which is to automatically compute
the gain based on the input frequency value. But the next UGen I want to make in the Duffing world is one that takes an
audio-rate input signal as the driver for the oscillator, and I'd rather there not be an implied low-pass on the input,
or having to set the gain to these really unusually huge values just to get reasonable response outputs. Lastly, I'm
worried that having these huge gains really color the output to be mostly the sinusoidal driver input, as it is so
much larger than any of the other inputs to the system.

Looking at the Tom Mudd Duffing oscillator I was a bit mystified because I don't see any huge gain numbers running
around, but then I notice that the integrator does a complete time step of 1 simulation second for every sample that
it integrates. Assuming a 44.1 kHz sample rate that essentially collapses the range of driver frequencies in the audio
range between 0 and 0.5, leaving the gain over that range much more. So I'm wrapping my head around how I could
scale time on the simulation, instead of scaling gain, because that seems to be the frequency range the Duffing likes
to hang out in. So that will be a project for tomorrow, although sample rates may not get me to a place where I can
keep the gain almost completely flat, which seems to be in the frequency range from epsilon to 0.25 Hz, which would mean
that the sample rate needs to be over 80 kHz if time steps are held to 1.0. At 44.1 kHz that would potentially two
simulation steps per sample, or perhaps one simulation step but a timestep larger than 1.0.

Speaking of, I did a comparison between my fancy Runge-Kutta-Nystrom pair integrator and a naive single-step integrator
and found no observable difference, outside of much lower CPU usage per oscillator on the single-step integrator, of
course. So I'm pleasantly surprised by that! It could also mean that I could swing a few integration steps per sample,
if needed. So I'm eager to code that up, and also to hear it on something other than laptop speakers!

