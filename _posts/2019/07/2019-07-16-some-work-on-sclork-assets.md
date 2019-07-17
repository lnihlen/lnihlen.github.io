---
layout: post
title: "Some Work on SCLOrk Assets"
date: 2019-07-16
tags: [ personal, sclork ]
---

Since I was feeling a bit better, and bit tired of just vegging out, so I thought I would dig in a bit to the asset
sharing system I recently pulled off the back burner for {% include tag_link.html tag="sclork" %}. A fair bit of
re-implementing and re-working after leaving the code for a long while. I think both I'm still finding my sea legs with
all this new-fangled C++ and also not remembering half of what I was intending with my designs.

A lot of retooling was around my integration with [flatbuffers](https://google.github.io/flatbuffers/). I've been going
back and forth on how to keep the serialization of the Assets and related structures efficient, with as few copies as
possible, and yet not ridiculously complicated or tightly coupled with dependencies. Still not happy with it but now
kind of in that mode where I just want to get everything going and I can worry about the finer points of optimization
once I've seen it all put together.

It's slow going but I got the asset adding to the database plumbed, and then started in on the asset read. Once I got
stuff moved around things started to move a little faster and flow a bit. I'm hoping that I'll be able to keep that flow
through the rest of the scaffolding.

