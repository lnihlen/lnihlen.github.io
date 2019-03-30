---
layout: post
title: "Last Work Day for a Bit"
date: 2019-03-29
tags: [ personal, scintillator ]
---

Super tired, particularly from doing radio yesterday morning and the lack of
sleep, but I'm looking forward to 9 whole days of not working coming up. The
Murder, She Wrote boxed set showed up so I'm busily working on ripping all of
it to the NAS downstairs so we can stream it to our various devices using Plex.
So that will be a fun project while I'm grinding away on
{% include tag_link.html tag="scintillator" %} in the coming days.

After Lillian's takeout Hil and I watched the latest RuPaul's Drag Race on the
couch while I noodled around with getting
[libshaderc](https://github.com/google/shaderc/tree/master/libshaderc)
compiling. The [Vulkan Tutorial](https://vulkan-tutorial.com/Introduction) of
course covers ahead-of-time compilation of the shaders, which is of course the
more straightforward option, but as I'm feeling a bit more confident about the
progression of the software development I'm taking deviations a bit further from
the tutorial if I think it will bring me closer to the target functionality I
need in Scintillator. The vision always has been that the code would assemble
shader programs from individual units, then send the whole mess to the shader
compiler at runtime, with hopefully a bunch of optimizations turned on. This
would happen around ```VSynthDef``` (or a pun name that I'm starting to think of
```ScinthDef``` which is admittedly terrible) time on a separate thread, which
is expected to be an asynchronous operation already, so can take a little bit of
time.

Vulkan may have a way to combine individual pieces of shaders in a single render
pass but I still would bet that letting the SPIR-V compiler take a crack at the
whole program will make for more performant runtime behavior. And I also have
the idea that folks might be able to provide (at least a subset) of some kind
of shader program directly to the synth from SuperCollider, so runtime shader
compilation is a must-have.

That said, I just introduced *7* additional dependencies to the synth, and am
significantly increasing the compilation time of the program as a result. At
least incremental build times will only be marginally impacted. And I basically
just brought an *entire compiler* into the project, which is pretty cool for an
hour's work or so chilling on the couch watching Drag Race.

