---
layout: post
title: "More Vulkan Setup"
date: 2019-03-30
tags: [ personal, scintillator ]
---

Had a couple of hours to make some headway on
{% include tag_link.html tag="scintillator" %}. While I'm still plowing through
the long list of Vulkan configuration code it's a good tour through all of the
capabilities of Vulkan rendering. Enormous configurability like this is pretty
cool in that it has a broad spectrum of creative possibility. The downside is,
of course, that there's just a *ton* of code required to light up that first
pixel. I'm at ~1500 lines of code right now in ```scinsynth```, all of it
devoted to rendering, and I've got another probably 500 lines to go before
that colorful triangle on a black background is visible in the window of my
own making.

To be fair, I did take a detour yesterday to allow for online shader compilation
but line-for-line that's probably the same length, given that the tutorial wrote
a short function to read the compiled shader bytecode from a file.

I have the ```VkPipeline``` object created and now it's time for the
framebuffers. Since the framebuffers depend on both swapchain and pipeline I'm
leaning toward having them be a separate object. Although I've done my best
to keep the different pieces separate and tidy there's just a ton of doodads
accumulating in the ```src/vulkan``` directory. So far there's:

  * ```Device```
  * ```Instance```
  * ```Pipeline```
  * ```Shader```, ```ShaderSource```, ```ShaderCompiler```
  * ```Swapchain```
  * ```Window```

And now I'm going to be adding ```Framebuffer``` and ```CommandBuffer```
objects. There might be some secondary organization here, like consolidation
of a bunch of these into a single organized unit, but I think for now keeping
these separate. My vision still is of a synth that starts up and opens up some
OSC endpoints, only. There's a high degree of configurability that goes in to
the creation of a render *context*, although if nothing is specified the system
will pick sane defaults for everything when asked to render sometihng. It
should be possible to create multiple windows or fullscreen contexts, talking
to different hardware potentially, and destroy them as needed. So, high degree
of configurability and a robust object life cycle. Both require a super well
thought through object design. Good thing, I don't have to figure it out
overnight.

I'm optimistic that I can have pixel flow in a few days, which would be super
exciting.

