---
layout: post
title: "SynthDef Build Process"
date: 2019-04-05
tags: [ personal, scintillator ]
---

More time at home today and more time to focus a bit on
{% include tag_link.html tag="scintillator" %}. I am discovering that my working
style has to vary a bit with also being the sole animal care provider, what
with Hilary out of town and all. The result is heads-down concentration at a
desk, even if it is located in the living room, is something that nobody in
the household is really used to. I could, if I wanted to, work from the couch,
which allows for the dynamics between the animals to eventually equilibrate on
some kind of group cuddle, and that can last until I have to get up to go to
the bathroom or some other interruption calls me away. But sitting at the desk,
nobody is used to that, so the animals wander from couch to kitchen area in a
constant patrol.

I think I'm also coming to the realization that learning an entirely new
graphics API, and a notoriously demanding one at that, while also figuring out
how SuperCollider does realtime audio synthesis, and applying learning from both
to inform yet a third new domain in the design of a visual synth is *actually
quite challenging*. I'm aware that progress is slow and I spend a lot of time
staring off in to space, just kind of digesting stuff that I'm reading.

That said, I dug in to more of the ```SynthDef``` build process for audio
synths on the SuperCollider code base, in the hopes that I could inform the
design of the bad-pun-but-its-growing-on-me ```ScinthDef``` code. Like many
things I'm studying in SuperCollider the simple path reads pretty
straightforward, but it also exposes some underlying complexity. One of the
big things that ```SynthDef``` does as part of the ```UGen``` chain build is
to pull out constants and parameters, for enumeration at the top of the Synth
Description file.

First was the decision to drop support for parameters for now. Understood that
this is an essential feature of any synth, the ability to tweak values at
runtime. Basically the feature that I have decided to defer out of the first
pass is the ability to provide *arguments* to the ```ScinthDef``` that can
be varied while the synth is running. It's painful but there's sufficient
complexity for here that this first pass of ```ScinthDef``` just completely
ignores them. So the only valid inputs for a ```VGen``` are going to be either
constants, output from other ```VGen``` objects, or *intrinsics*, a term I'm
using to describe variables that exist because they are required for the
graphics pipeline to function correctly, like vertex or fragment coordinates.

On that last, the intrinsics, they may go away because it seems that Vulkan
really makes no assumptions whatsoever about what your pipeline gets up to,
which is awesome but then perhaps the presence of an intrinsic in the ```VGen```
chain could simply be a sign to the synth that it is something that it should
compute.

So after pushing some code around the plate for a bit I thought perhaps a
different tack to help focus through all this ambiguity, fear, and doubt would
be to write the format for the YAML output file I want the ```ScinthDef``` to
ultimately generate for the synth to consume.

This was helpful, although it again took longer than might have been strictly
necessary, due to agonizing about the decision to drop parameters, frequent
interruption by the ever-charming Molly for tug-of-war or cuddles, and quite
a bit of jamming on Cuphead (if I'm entirely honest). It wouldn't be a vacation
otherwise.

There's also the question right now of an *output* ```VGen```. The optimization
steps in ```SynthDef``` are aware of output-capable ```UGen``` objects, and
mercilessly prune signal chains that don't result in output. Without
multichannel expansion I have defined a lone ```VOut``` object, supporting
```.fg``` output only (although it is interesting to think of what vertex output
would look like.. like maybe wireframe?). There's so much more to do in this
area too that I'm already deferring. I'm going to start making some rough
milestones over on [GitHub](https://github.com/lnihlen/Scintillator) and track
them there. If nothing else, it will help manage my anxiety about cutting stuff,
because I can put it on the list! Of course, this gets me in to some trouble
because there's currently two different repositories, and I'd like to track
code across both. What I might do is deprecate the standalone Synth repository
and move everything in to the Quark. It's going to be a heavy Quark, but at
least everything will live in one spot.

With the first crack of the spec done I'm hoping to generate some test YAML
tomorrow, and then it's time to take a trip back to the C++ side of the house
to start doing something interesting with that input file. At least there's
plenty of known work here, along with all of the uncertainty and doubt.
Following that thread of things I know I will need to do, along with making
peace with the fact that many things may have to ultimately be re-done, will
be the path through this valley of shadow. At least, it's never lead me astray
before.

