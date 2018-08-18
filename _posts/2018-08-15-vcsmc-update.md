---
layout: post
title: "vcsmc update"
date: 2018-08-15
tags: [ vcsmc, i_made_a_thing ]
---

It feels fitting, and some continuity with my old blog, to have an early post
here be an update on my perennial hobby project
{% include tag_link.html tag="vcsmc" %}. To date I've built a system that takes
as input an image describing a single frame of video and then uses Evolutionary
Programming to output a resultant binary blob that contains VCS binary to drive
the CRT beam through one pass
of its beam from top to bottom, programming the state machine on the video
hardware to generate something vaguely resembling the desired frame image.
Computing a single frame takes significant time (hours) and the final results
are, well, underwhelming:

<iframe width="560" height="315" src="https://www.youtube.com/embed/kehRkaTLLg8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

As stated these images take a huge amount of time to generate, and there's a long
period of stagnation at the end of each frame generation where the EP algorithm
is stuck in some local minimum. I've been using for an error function a mean
error distance between individual pixels using a human visual system weighted
color distance metric,
[CIEDE 2000](https://en.wikipedia.org/wiki/Color_difference#CIEDE2000). That's
the rough state of the algorithm that generated the video above.

I wanted a better signal about actual visual difference between target frame and
the generated frames, so I implemented a version of
[SSIM](https://en.wikipedia.org/wiki/Structural_similarity), which on the whole
does generate better imagery but added huge compute times for the frame
difference computation. I then tinkered with adding GPU acceleration, settling
on using CUDA, only to discover later that I had rendered my primary development
laptop useless because it has an AMD card inside. Whoops. The project has mostly
stalled since then, with a couple of intermittent crashes rendering the
computation of a nontrivial video sample intractable.

But I've been recently contemplating another reboot of the project, with the
following tasks in mind:

1. **Update the dependencies.** Clean house on the ones I no longer need. I know
there are newer versions of these things floating around.

2. **Uncomplicate the kernel program generation.** Right now every candidate
frame image program, called a *kernel* in vcsmc parlance, includes logic to
render the embedded audio for that frame (by directly modulating the voltage
on the audio DAC twice per scanline) as well as bank switching logic, because
the frame programs invariably consume more than the 14 bits of address space
available to the VCS. It seemed a good idea to always generate valid VCS
program code, but the resultant kernel code is pretty complicated. Rather than
working so hard to guarantee program validity during kernel generation I'm going
to apply the necessary bytecode in the frame as an write-over patch in a single
pass after generation.

3. **Build caching into the score evaluation from the beginning.** Looking at
kernel images from generation to generation of the Evolutionary Programming
algorithm there are usually only a few pixels changed. However the current code
scores entirely from scratch each time. Rather we should tile the images and
cache tile scores based on a fingerprint of the generated image tile.

4.  **Bootstrap intraframe image fitting with previous frame image.** Another
form of caching, allowing non-key frames to converge to something much faster.
I've long thought of this but also had concerns around it - namely that the
last frame in a key sequence might have higher quality than the first, as its
had a lot more fit time, or that we might be trapped in a local minimum and
a fresh approach to each frame might guarantee higher quality. But given that
frame generation is taking *literally hours* this seems like a secondary concern.

No idea when I'll get around to this stuff but good to write it down.
