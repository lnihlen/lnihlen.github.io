---
layout: post
title: "SCLOrk Hack Day 2"
date: 2018-12-18
tags: [ personal, sclork ]
---

Today was much better than yesterday in terms of productivity and output. Last
night, after the holiday party I was able to get the laptop to come back from
complete power drain. I had some time so I started a new approach on the
`SyncTempoClock`, this time just inheriting from `TempoClock` with an extra
task to set the value of `beats` periodically based on the values coming from
the `ClientTimeBase`.

This result showed good promise last night, and I was able to code up a working
version of it this morning within an hour of arriving in the
{% include tag_link.html tag="sclork" %} rehearsal space. Then we spent some
time testing it out on multiple laptops. It felt great to see the code working
well with the kind of synchronization that we had been trying to achieve for
weeks.

I have a worklist of things to follow up on, including a rewrite of the chat
program away from Utopia and with a redo of the UI. But I feel like the rest
of the code I want to crank out by the end of the year is what we'd call I
[SMOP](https://en.wikipedia.org/wiki/Small_matter_of_programming), or Small
Matter of Programming. But I mean it in the un-ironic sense, like basically
there's bunch of code to crank out but I'm not anticipating I'm going to have
to be digging through interpreter source code or making big compromised to
my code in order to get things to work at all.

When I got home Hilary remarked that she's continually surprised that I can
happily hack away for 8 or more hours in a day, with no real breaks, and then
be fine coming home and programming some more. Yeah I guess that's not normal?
But I swear I'm having fun..

