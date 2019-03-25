---
layout: post
title: "Some Work on Scintillator"
date: 2019-03-24
tags: [ personal, scintillator ]
---

Telling Brian and Nathan, SuperCollider heroes, of my plans to build a visual
synth with tight integration with SuperCollider has been a definite kick in
the trousers to make some progress on it.

So, while I'm still totally fried I was glad to make some small forward progress
on {% include tag_link.html tag="scintillator" %} today. I am going slowly
through the [Vulkan Tutorial](https://vulkan-tutorial.com), but I've always sort
of disliked the C++ paradigm of a nearly empty main.cc that just invokes some
```Application``` sort of object and that's where the main action takes place.
So I've been taking the individual lessons and flattening them all into
```int main()```, with the intention that once I have a better handle on what
the individual parts of the *highly* configural Vulkan setup process I want
to encapsulate into objects, perhaps that are controllable by the client,
and how generally the system should be organized to allow for the right kind
of flexibility while still maintaining a logical organization.

Now I'm getting into the specifics of configuration a swap chain and am starting
to regret my initial decision, at least a little bit. One could argue that while
I don't care for the Application object design pattern, it is at least *a*
design, whereas just dumping everything in main is most definitely not a
design, or at least one that scales elegantly with any sort of complexity.

This is exploratory coding at this point, I think the last big conclusion about
the design phase was that while I had developed some initial concepts that felt
promising I had a lot more to learn aboutu Vulkan and its conceptual framework
for graphics programming before I could proceed with any additional detail in
the design.

There's this trying phase in graphics programming which is getting to first
pixel lightup. And, while Vulkan has many strengths it is exceedingly verbose
when it comes to hardware discovery and configuration. Building out a huge
system for hardware enumeration over OSC to the SuperCollider language, and
allowing for incredibly detailed device configuration from SC would be really
cool, but I would argue that getting to a place where I can see my first
```ScinSinOsc``` animate at 60Hz with hardware acceleration would be a much
more meaningful milestone. That's the first vertical slice, being able to
light that up with a ```ScinSynthDef```, and we can expand outwards from there.

All these names are TBD, by the way. I haven't settled on a naming convention
on the SC side. I would love to just use the ```Sc``` prefix but that seems
uncomfortably close to SuperCollider's own ```SC```. Adding the next character
gives ```Sci``` which too obviously leans towards scientific computing. So
that's how I arrived ```Scin``` as a prefix. There's also just ```V``` in front
of common SuperCollider things, so like a ```VSinOsc``` versus a ```SinOsc```,
but there are a few objects in SC already with a ```V``` prefix, and in those
cases its consistently being used to indicate variable-rate audio stuff. So
then there's ```Video``` or ```Vid```, or ```Vk``` for Vulkan but the former is
way too generic and I think the latter far too specific, for most Vulkan is
likely to be an implementation detail. Hence ```Scin```, the least bad option.
Maybe ```S10r```, like they do with ```i18n``` for ```internationalization```?
Ugh. I do like the term ```VGen``` for video generator objects, similar to
```UGen``` for *unit* generator objects on the audio ```scsynth``` side. So
Sometimes I find myself swinging back to the ```V``` convention, and I might
stick it there. It's something to worry about later, still very plastic, but
once a bunch of code gets written it gets increasingly difficult to change so
I'm thinking about it now.

In terms of device configuration, I've been thinking of a system that boots up,
intializes stuff, opens up OSC ports, and then just waits for further
instruction. It can provide an enumerated list of supported hardware and
device configuration options. Then I can write SC code to both expose this in
code as well as some nice UI options. What I want is some kind of way to ask
ScintillatorSynth what options are available, and to have some kind of say
in creation of windows (or fullscreen displays), their dimensions and color
parameters, and then be able to create as many output pathways as seem logical.
Each of these would be organized into an overall unified output buffer sort
of ```VGen```, probably named ```VOut```, with a similar concept of there
being busses for video data just like there are for audio data, maybe accessible
via index.

Of course, there are also sane defaults, and barring any additional
configuration ```scinsynth``` could just boot up and show a small preview
window that accepts 3 (or 4) output channels, one each for red, green, and blue,
or possibly some other color spaces, maybe YPbPr or HSV. Maybe hue is mapped
from -1.0 to 1.0, as are all the other channels by default (to keep parity
with SC audio channels), and so some SuperCollider code like:

```
{ VOut.pr(VSinOsc.pr) }.view
```

Would show a sine wave in color at full saturation and value oscillating at
1 Hz in a small preview window popup. Note the ```.pr```, short for *pixel*
rate, meaning that the function should be evaluated at every pixel, instead
of ```.fr```, which would be *frame* rate, meaning that the function is
evaulated every frame, probably evaluated on the CPU and provided to the shaders
as a uniform.

This does represent a substantial difference, even in arguments, between what
```.fr``` and what ```.pr``` to the image and what that represents. For example
I would expect the entire image to maintain a uniform color and that would
animate through the hue color space at 1 Hz. Furthermore, arguments to phase
and frequency that were a function of virtual pixel coordinates would not
be acceptable in a ```.fr``` call, whereas within the ```.pr``` call that
will kind of be the whole point, and in fact the default will be to use the
radius in the phase argument.

But I'm getting ahead of myself. I think for now ```scinsynth``` will open
a non-resizeable window on invocation and will keep it open for the duration
of the synth lifetime. If I can get there within a month I'll be impressed
with myself. Time to press on through the swap chain stuff and on to lighting
up some pixels!
