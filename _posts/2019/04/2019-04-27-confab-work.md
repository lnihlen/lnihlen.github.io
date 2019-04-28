---
layout: post
title: "Confab Work"
date: 2019-04-27
tags: [ personal, sclork, supercollider ]
---

Hil and I had been planning to head over the hill into San Jose to shop for some essentials for my upcoming trip. But,
after a brunch at Saturn, Google Maps was predicting a close to 90 minute trip in to town. It looks like maybe some
construction or an accident (or both) on the 17.

I didn't think spending over an hour in the car just to go shopping seemed like a wise use of our time so we just got
groceries locally and headed home. I was quick to cloister myself in my office then, wanting to focus on my latest
project for {% include tag_link.html tag="sclork" %}, the asset sharing system for easy sharing of all sorts of things
from right inside of {% include tag_link.html tag="supercollider" %}.

The C++ code is great fun to work on, and the project is starting to pick up a little bit of momentum, with some time
spent today actually writing code that will do production things, instead of problem solving with project infrastructure,
dependencies, or tools. I now have documentation and tests building automatically along with the source code, and errors
in either will be treated as fatal errors in the project.

There's some annoying difficulty with getting ```glog```, the [Google Logging Library](https://github.com/google/glog),
to play nicely with ```gflags```, the [Google Flags Library](https://github.com/google/gflags). I'm getting an error on
CMake Makefile generation:

```
CMake Error: install(EXPORT "glog-targets" ...) includes target "glog" which requires target "gflags_nothreads_static" that is not in the export set.
```

Not too sure what that is all about. I've fiddled with the build configuration for ```gflags```, and this was as far as
I could get. The error seems to happen after ```Makefile``` generation, so I am actually able to compile things still,
but it wrankles. I haven't been using CMake to generate any kind of install step, and I don't really plan to. I think
since all of this C++ code lives inside a quark, and I'm statically linking the binaries right now, I would be fine
with everything just living right where CMake builds it, and even coding the Quark to assume the same path to the
C++ binaries by default as well.

CMake fiddling aside, I *was* able to get a first record read/write going with
[LevelDB](https://github.com/google/leveldb), and both parse and emit some YAML with
[yaml-cpp](https://github.com/jbeder/yaml-cpp). I'm covering all the classes with Doxygen, and the build fails if
something is un-or-underdocumented. I also wrote a trivial data container class and used it as a bootstrap to bring in
some unit testing using [googletest](https://github.com/google/googletest).

So all in all a really fun and relatively productive day. I'm hopeful the traffic situation in to San Jose will be a
bit better tomorrow, and also Hilary was thinking the dogs would like a trip to the beach. So not anticipating that I'll
have the same kind of time to invest in at the workstation, which is probably a good thing. All things in balance, and
it'd be nice to go out to "the big room," as the old Hacker's Dictionary (back when books were only available on print)
referred to places outside as.

