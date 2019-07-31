---
layout: post
title: "The Slow Path"
date: 2019-07-30
tags: [ personal ]
---

So I think what's driving me a bit nuts is that there really isn't any fast path, at least not one that I'm aware of, to
becoming an excellent people manager. And, unlike software engineering in general, I'm a lot less aware of any tangible
improvement in my skills. You don't get the kind of feedback from a team that you get from a compiler or performance
metrics. Furthermore, the kind of problems I face at work are *hard*, like I don't often know what the next steps might
be or how best to be helpful. I enjoy a challenge, I really do. And I just hope that I am actually improving at work,
because things certainly aren't getting any easier. I'm re-adjusting my expectations of what a managerial progression
timescale looks like, from something on the order of quarters to something on the order of years.

On the {% include tag_link.html tag="sclork" %} front I was able to get data flowing between client and server today.
I'm starting to think through the two remaining large features I think I will need in order to get a revision of
SCLOrkChat over to the new asset system; *lists* and *names*. Because Assets can't be revised (it changes their hash,
therefore violating the one immutable part of Assets that their key identifier is always a hash of their contents),
without built-in list support there isn't an elegant way to maintain persistent lists of other assets. Names provide a
mutable reference to an Asset that allows for me to hard-code references to Assets of importance to the system without
having to hash them first, and again allowing the data referenced by that name change Assets as it is modified.

Looking forward to tomorrow's deep working session to see if I can push that forward a bit more. Step by step, day by
day. Grit as gained from the grind.

