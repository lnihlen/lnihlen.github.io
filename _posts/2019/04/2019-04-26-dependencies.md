---
layout: post
title: "Dependencies"
date: 2019-04-26
tags: [ personal, sclork, supercollider ]
---

I'm really digging all of the neat libraries I've been able to dig up on this latest project for
{% include tag_link.html tag="sclork" %}, the asset database. The C++ part of the code I'm calling ```confab```, which
is a nifty REST endpoint that connects with other mirrors just like it in a tree of caching and file distrubition, while
exposing an OSC port for communicating with the {% include tag_link.html tag="supercollider" %} wrapper classes I'll
eventually write. I like this pattern of offloading stuff that has little to no support within the SuperColider language
itself to C++ binaries, which then SC can boot up as needed and talk to using OSC.

Speaking of, It probably will make sense at some point soon for me to write a C++ implementation of the SCLOrkWire
UDP utility class I wrote for SC, just so that interop between the two languages is super straightforward and both
sides are speaking the same language.

All that aside, there's just *a ton* of really neat tools out there to facilitate this project. For persistent storage
I'll be using [LevelDB](https://github.com/google/leveldb), from two nerd superheroes inside of Google, Jeff Dean and
Sanjay Ghemawat. This is a fast file-based key-value store, allowing us to add a ton of assets like images, code
snippets, and even audio samples, to the database yet allowing the system to scale elegantly.

Speaking of Google projects, I've already pulled in [gflags](https://github.com/gflags/gflags) for dead simple command
line parsing, and I have a suspicion that we'll be seeing the unit testing tools
[Google Test](https://github.com/google/googletest) and Google Mock (which lives inside of the testing framework) very
shortly. And definitely I'm going to want [Google Logging](https://github.com/google/glog) right away, I got used to
it working on Chromium and miss it dearly whenever it is not around.

I'm also adding [Doxygen](http://www.doxygen.nl), not only for the nacsent confab design document but also for the more
traditional usage of documenting the code I'm writing in C++. As I said in an earlier blog entry, having the integrated
help system inside f the SuperCollider IDE has raised my expectations about self-documenting code, and just like how
writing tests (for me) makes the coding and API design more clear and elegant, I'm finding the same when documenting the
API. Nothing like "thinking out loud" in plain old English about the code you're writing to help clarify what exactly it
is one is trying to accomplish.

Besides automatic documentation building I'm also looking to bring over the same code style and automatic formatting
tools we've been developing over on SuperCollider. So ```clang-format``` is likely to be shortly making an appearance,
and another format cleanup CL shortly to follow.

Some of the data inside of the database I'd like to serialize in Base64, and the keys for the assets are based on a
hash of the asset data itself. Well, I was already using [xxHash](https://github.com/Cyan4973/xxHash) over on
{% include tag_link.html tag="vcsmc" %}, looks like that is still a pretty darn quick non-cryptographic hash, and
somebody wrote a slick [SIMD accelerated Base64 encoder](https://github.com/aklomp/base64) that's also very quick.

Oh, and for sending multi-part or bigger files between Confab instances I've got my choice of a bunch of different
compression algorithms, maybe I'm leaning towards [LZ4](https://lz4.github.io/lz4/) right now but we'll see. And there's
even [Twitter's Emoji](https://github.com/twitter/twemoji) library for when I get to the stage that I want to test
zinging assets around by adding emoji support to SCLOrkChat.

Super cool to see all this badass stuff in open source! It's going to make working on confab this weekend a lot of fun
and (hopefully) actually somewhat productive.

