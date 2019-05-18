---
layout: post
title: "More Parsing Headaches"
date: 2019-05-18
tags: [ personal, supercollider ]
---

Hilary and I spent the morning walking through first the National Portrait Gallery, followed by the general National
Gallery. It was incredible and overwhelming. I saw art by Van Gogh, Sanger, Turner, Pissarro, Monet, and on and on.
Truly a feast for the eyes. Then we grabbed Indian food at a small vegetarian place around the corner from the museum,
and it was again delicious and spicy. I'm beginning to understand why many of my East Indian colleagues at work politely
won't comment on the quality of Indian food when dining out in the United States.

I think Hilary is coming down with a cold, unfortunately, so we returned to the hotel room for some rest and I dug in to
the parser in earnest. I swear I've written the same few hundred lines of code four or five times now, but the latest
architecture I'm settling on is finally starting to feel useful. I've learned something each time but it is very slow
going. One of the problems here too is that the expressiveness of the whole language of SuperCollider means that it is
very difficult to write just a teeny part of a parser without it pulling in most of the other language as a requirement.
In other words, it's been tough to validate the little parts I am building without either feeling the need to cut so
many corners on the validation it starts to feel like I am only validating the test instead of the code, or to implement
the whole thing and just hope for the best.

I think, however, that I'm now on my way to finding a happy medium on that and can start writing some focused
```UnitTest``` test cases that check useful things about the processed output parse tree, particularly in the area of
whitespace assignment validation. This is the tricky problem of injecting parse nodes to handle whitespace, and making
sure that they are being inserted into appropriate places in the parse tree so as to appropriately indicate the correct
containment. So, for instance, the newline character between the opening paren in a block should be assigned to the
block generally, but the newline between the first variable declaration and the second variable declaration should be
assigned to the variable declarations subblock, but the newline after the second variable declaration and before the
first imperative statement in the block should probably go back generically to the block parse node. And so on. Unit
tests in these situations will help ensure sanity and consistency as I go on to implement the support for the *30* or so
reamaining node types the native parser emits.

Of course, by the time I felt I was finally in this good groove and ready to write a few meaningful unit tests I noticed
it was almost midnight and I had yet to start on this blog. And Bruno sent out an email saying that there will be time
for only a few rehearsals between now and the Garden of Memory gig at the end of June for {% include tag_link.html
tag="sclork" %}, so I'm not sure I'll have the next generation of the SCLOrk software ready by then. In fact, seeing as
how I am now completely captivated by this parser work I'm going to go ahead and assume that I won't be ready, but
should keep ploughing away on this stuff because it's fun and also I think (or at least hope) going to be pretty useful
to the general SuperCollider community. Nothing like a spiffy new metaprogramming tool to really spice things up in a
programming language, yeah?

At some point in the afternoon when I had hit peak aggravation with the parser work I took a break to read through some
more of the documentation on my static hosting ISP and managed to get both [solitarybees.us](https://solitarybees.us)
and [scintillatorsynth.org](https://scintillatorsynth.org) up with valid SSL certificates and serving "Hello, World"
pages out to the Internet. Then I spent a while poking through a variety of different static site generators, because
apparently static HTML sites are the new hotness. I've been feeling like my JavaScript programming is very much out of
date and boy did looking through some of the React.js stuff confirm that intuition in spades. ES6 is like a whole new
programming language, and it seems that many cool things are now wihin easy reach of the modern JavaScript developer. So
far Gatsby is the front runner for a candidate for the next site I build, and of course the plan is once I settle on
tooling for one of these other sites I'll be turning my attention back to the blog for a conversion to that and a
re-home out of GitHub and in to a private repository and hosting arrangement where I've got more customization options
and control.

But all that's for another day.

