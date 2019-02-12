---
layout: post
title: "Some (Limited) Halide Success"
date: 2018-10-07
tags: [ vcsmc ]
---

Slept in, loaded the dogs in the car, drove over to Coffee Cat and got an Oat
Milk Latte, then rolled to the beach. It was a beautiful, clear day, with
fairly big waves crashing in, lower tide meaning plenty of open beach, and
almost noone out.

Then it was back home and time to dig in to the `Generator` code doing RGB
to CIEDE LAB conversion using Halide. I finished the modifications to the build
system to allow for Ahead-Of-Time compilation of the `Generator` and then spent
a bunch of time trying to get a `Halide::Buffer` to do anything like the
documentation seems to suggest it can do.

Turns out, after much Googling and reading of various StackOverflow articles,
there's a `Halide::Runtime::Buffer` which is the `Buffer` you *actually* want
to use when you are trying to *actually do anything* with all your pretty Halide
code. Ok.. After getting that to work, a Google of `Halide::Runtime::Buffer`
turns up that one of the tutorial files on Halide actually uses this, but not
in the pretty formatted tutorial file on the website, rather a supporting file
*referenced* by the pretty formatted file.

A little debugging later and I have passing unit tests! Always satisfying when
something
[comes together](https://github.com/lnihlen/vcsmc/commit/80e64128ac1650d2b98ca22eb1a367aaf4c2b240)
after some hard work. And given that it's only shortly before bedtime on Sunday
evening, with Hilary returning tomorrow as well as a full work week ahead, the
timing couldn't be better.

