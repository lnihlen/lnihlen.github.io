---
layout: post
title: "SCLang Parser"
date: 2019-01-18
tags: [ personal, sclork ]
---

Finally had some time on Thursday morning to think about the
{% include tag_link.html tag="sclork" %} stuff and ended up drawing the
conclusion that I should start work on a (specialized, for now), SuperCollider
language parser, written in SuperCollider language itself.

This is really a terrible idea. The problem is that I want to build a UI that
would ultimately allow for round-trip engineering from code to UI and back
again, meaning that users could edit parameters of a ```Pbindef``` directly as
code, or manipulate a slider or other such UI elements to interactively change
those values. Changes to one would be interchangeable to the other.

Perhaps unsurprisingly to some, this turns out to be pretty challenging.
Additionally, the SCLOrk group was hoping to have some kind of working prototype
available for use in rehearsal this coming Monday.

There are some artificial constraints here that I'm chafing at the idea of
removing but might have to. The situation is this - Bruno, the conductor of
SCLOrk, has asked folks to write a series of ```Pbindef``` patterns that
muscially invoke interesting snippets selected from a common sample library.

This was originally a pure coding exercise, with each member of the ensemble
invited to submit one or more "presets" consisting of multiple of these
```Pbindef``` statements intended to be played together as a collection of
"voices."

The original goal for the UI was to allow a user to specify a player number at
startup, then select a "preset" with their individual player number mapped to
a voice. The UI would then offer facilities for interactive manipulation of
certain parameters, or if desired, could provide the raw source code of the
```Pbindef``` for direct manipulation.

Which leads us to our first challenge. Because folks were asked to compose
short pieces of music using SuperCollider code, naturally (and reasonably),
the ```Pbindef``` statements written reflect a diversity of different approaches
to providing values. It's the kind of thing that can be maddening to parse,
lots of cases where the input is uniform, except for one or two special cases
on each part of the input.

This means that the parser has to become also very full of special cases, and
the return on engineering investment for each special case is low, and there's
no quick, obvious way to get to a place where 90% or more of the code written
to date could be quickly parsed.

Since the only input requirement was valid SuperCollider code this sort of lead
me to the place where I thought perhaps there might be some way to re-use the
parser inside of SuperCollider itself, but as far as I can tell while sclang
does indeed offer ways to interpret strings as code, and execute whatever they
contain, I don't see any obvious way to extract something like a parse tree
or perform lexical analysis or anything like that. This seems to me a missed
opportunity - things like automatic code refactoring and static analysis benefit
greatly from being able to parse their own language, inside the language.

It's obvious to even me that I'm off in the weeds whenever I start thinking
about some major new changes to SuperCollider in order to build a quick UI
to help us better perform a piece.

