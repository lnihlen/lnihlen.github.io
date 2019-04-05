---
layout: post
title: "Four Hundred Meter Mosey"
date: 2019-04-04
tags: [ personal, scintillator ]
---

A little more motivated today so my time was divided between playing Cuphead
and Valkyria on the Xbox and hacking on
{% include tag_link.html tag="scintillator" %}. On the former I need not comment,
and on the latter I'm currently traversing a vague valley where I discover a
bunch of requirements and unanswered questions, and try to make some arbitrary
decisions about what a first draft might look like, knowing that much of what
I'm writing is probably wrong.

The new plan is to work on the SuperCollider side until I can get to a place
where I can generate a chain of objects, from constants or *intrinsics* like
vertex positions, through processing and finally out into monochromatic color.
This ```ScinthDef``` will serialize to a YAML file. I'll generate a few test
cases of that, then turn my attention to the Scinth code, which will take a
SynthDef on start, convert it to a fragment and vertex shader, then try to
render it on screen.

This "thin vertical slice" approach I'm hoping will crystallize a lot of the
open questions around design and signal flow. There's lots left to do, even
just basic pieces to build, like being able to define more than one ScinthDef
and play them, but everything else feels like it builds on top of the basic
stuff defined in this slice. So that's where the work is going for now, when
the work happens.

I wrote some unit tests for ```VGen``` that validate that I'm assembling the
same sort of signal chain data structures that are produced in a ```UGen```,
if much less sophisticated. I'll be growing that a bit further, adding some
fundamentals like ```VMulAdd```, which the audio equivalent ```MulAdd``` neatly
optimizes itself away during construction time as needed, and then I'll switch
my attention to ```VScinthDef``` and some associated unit tests. Construction
of that should allow for the YAML serialization to a file, which remind me that
I should also start work on the ScinthDef YAML specification documentation.

One of the tricky things that still feels a bit wide open is the separation of
vertex-rate ```.vx``` operations into the vertex shader, followed by
fragment-rate ```.fg``` operations in the fragment shader. So it's a toplogical
sort of the output graph back to the inputs, thinking about pushing stuff to
the vertex shader (computed per-vertex, so much cheaper) whenever possible.
But the information flow is from vertex -> fragment, so once we've gone to the
fragment shader vertex rate computation has to be reconfigured to fragment.

It's funny to leverage some of the discussion around rate from SuperCollider
to Scintillator. Modern thinking on SC is that rate distinctions don't really
matter as much as they used to, but they definitely do on the card. For the
simple case where I'm drawing a single quad on the screen using an index buffer
the vertex shader is going to execute 4 times, once at each corner, or possibly
6 times at most for the corners where the two triangles meet. The fragment
shader code is going to execute for every pixel in the output buffer, which on
a 4K display is 8.29 *million* times. So yeah, pushing things into vertex
evaluation, when possible, can make a lot of sense, and then relying on having
some control over interpolation of the values as they appear at the fragment
stage.

For the first slice there are some things you get for free on a basic rendering
of a quad, which I'm calling the *intrinsics*, such as the xyzw coordinate set
for each fragment, which is basically the ```gl_Position``` as specified in the
vertex shader. But otherwise for the first slice we'll assume most everything is
happening at the fragment shader stage. Simple as possible for the first slice.

I'm also trying my best not to get lost in concerns about the output format and
data structures, so hence the decision to go monochromatic. I'll probably for
now skip all the multichannel expansion stuff that I'm envisioning goes with
color synthesis. It's sort of like stereo or higher-channel audio but in this
case we get 3 or 4 channels for RGBA color output.

Once we have actual Scinth scheduling going on my vision is that every Scinth
will render to its own framebuffer, then the swap chain is clearing to a
predefined clear color and then alpha blending in the framebuffers from the
various synths. But again, all for later.

Tomorrow I'll continue the push for YAML serialization.

