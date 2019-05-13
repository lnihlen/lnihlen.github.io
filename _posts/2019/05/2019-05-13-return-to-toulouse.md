---
layout: post
title: "Return to Toulouse"
date: 2019-05-13
tags: [ personal, supercollider ]
---

Up after "a bit of a lie-in" to catch the second van out of Aulus-les-Baines and back to Toulouse. After 5 days in the
countryside the noise and population density of the city felt quite overwhelming. Some of the others in the van were
talking about finding some lunch together but with the overstimulation I was feeling, and the multiple pieces of luggage
I was handling, it seemed like a better call to grab a taxi to the hotel and try to get checked in.

There was a wait for the room to get ready so after some lunch I sat a bit and dug in to the parser work on
{% include tag_link.html tag="supercollider" %}. I think the real challenge of the work is starting to become apparent,
as I wrestle with the results the parser is producing. It seems to be a combination of a parse tree that is
purpose-built for the compiler, so may not have the most obviously usable parse tree for my purposes, and my own
learning curve on understanding the (entirely undocumented, natch) output from said parser.

In any event, I spent a few hours tinkering with the output format of the code that marshals the parse tree from C++
over to SCLang land, and then printing out the results to the SCLang terminal, trying to understand what I'm looking at
and how I could turn it into something useful for a tool like an automatic code formatter. Brian, one of the primary
maintainers of SuperCollider, had been discussing the idea that the parser tool could produce "round-trip" parsing,
meaning that the tree output of the parser could be modified (say adding or removing whitespace) and then usefully
reprocessed back into a valid source code string. This has become an organizing principle for the work, but despite
some significant time tinkering with the data I regret that I'm not much further toward that goal. At least the parse
trees I'm looking at are starting to make some sense to me, but only just.

Once the room was ready I took a nap of two or three hours, then up for some dinner, then more work on SuperCollider.
I was increasingly excited by the prospect of Hilary arriving from the airport, and she did around 9:15. As she
was totally exhausted from her travel overseas we both went to bed shortly after our reunion.

Tomorrow is our first day together in France!

