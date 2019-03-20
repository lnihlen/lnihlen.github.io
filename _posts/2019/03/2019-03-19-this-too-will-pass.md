---
layout: post
title: "This Too Will Pass"
date: 2019-03-19
tags: [ personal, scintillator ]
---

We've definitely hit the point in the perf cycle where I start questioning my
life choices. It's just the grind getting me down, but I get scared that this
is the new normal, returning home after a long day of work each day, with
time to spare only for quick dinner with Hilary, a mad dash through any
oustanding homework items due the next day, maybe an hour of downtime, then
bed.

I'm dreaming about working on {% include tag_link.html tag="scintillator" %}
on my commute, and have written some rambly early design documentation which
is currently checked in to the Scintillator Quark
[repo](https://github.com/lnihlen/Scintillator), but is exploratory enough that
I'm halfheartedly considering moving the discussion over to a longer blog
post here.

It's also time to get serious about Vulkan, because the design of the video
synth is likely to be strongly influenced by the needs and particularities of
the Vulkan imnplementation. I remember learning OpenGL back in the 90s (dating
myself a bit here) using the big Red Book and the GLUT toolkit that took care
of some of the setup boilerplate.

I understand Vulkan is a lower-level graphics API that offers a great deal more
flexibility and control to the programmer, and the cost of that increased control
will be increased complexity in the API, but boy howdy that's a whole lotta
setup code! The [Vulkan Tutorial](https://vulkan-tutorial.com/Introduction) is
also using [GLFW](https://www.glfw.org/), the same cross-platform setup library
I'm using. So the next big goal for Scintillator is to get through that and
then get a simple ```VSinOsc``` rendering at 60Hz in a window.

Then I'll switch gears and start trying to get some OSC control over the
situation. The first major milestone is to be able to boot up the
ScintillatorSynth server, create a ```VSinOsc```, and then vary its parameters,
all from the SuperCollider IDE.

At that point it'll be about building the synth graph, adding new ```VGens```,
and other features like image + video encoding and decodes, possibly alternate
color spaces, robust documentation, and on.

I was saying that transitioning to management full time at work is one of the
best things that has happened to my recreational programming activities. And
lucky for me, there's plenty of work ahead of me on this project, and plenty
of management work for me at work.

Now, if only Hollow Knight wasn't so fascinating..  And the sequel looks really
rad too!

