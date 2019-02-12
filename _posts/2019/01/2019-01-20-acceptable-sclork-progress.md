---
layout: post
title: "Acceptable SCLOrk Progress"
date: 2019-01-20
tags: [ personal, sclork ]
---

So today was, after sleeping in and making waffles, all about trying to get out
of that hole I put myself in on {% include tag_link.html tag="sclork" %}. The
idea of building a parser for the sclang code lurking inside of the preset
files written by students did have me a bit gobsmacked.

I broke the job in to multiple phases, first building a tokenizer and then
taking the tokens and building them into voice parsing using a state machine.
That scenario where I was worried that there were going to be a lot of special
cases did occur, but by keeping the two phases distinct I was able to expand
coverage incrementally. I went from successfully parsing 2 of the 28 preset
files, to 10, to none (bad bug), to 27. It turns out Bruno had a
specially-named preset that adds some additional complexity that none of the
other preset have, that would take a lot of additional work to parse, so pausing
on that one for now.

Thinking that was good enough, I turned to the UI. I was able to get a
rudimentary build-out of the preset selector. I think this could be enough to
get us started tomorrow, modulo testing and a few extra "bells and whistles"
I have in mind.

But at least the core is there. We're up early tomorrow, despite the vacation,
to take Hilary's car in for service. So I should have time to hack away before
rehearsal. I've known for a while how dangerous down-to-the-wire hacking can be
but there just really wasn't enough time on this one. I might consider pushing
an early tag tonight of the [SCLOrkPD](https://github.com/lnihlen/SCLOrkPD)
repo, just to make sure there's some kind of fallback in place, so that when
I'm hacking away tomorrow and everything goes to crap I can at least ask folks
to go back to the old version.

Fingers crossed for tomorrow!

