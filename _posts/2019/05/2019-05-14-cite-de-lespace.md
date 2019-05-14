---
layout: post
title: "Cité de l'espace"
date: 2019-05-14
tags: [ personal, supercollider ]
---

Hilary I think is still a bit jetlagged, so woke up super early, but was kind to let me sleep in until a reasonable hour.
We did the breakfast buffet, which is delicious, and then went for a long walk around Toulouse. I took Hilary on the
same route that I had soloed originally when here before the trip to Aulus-les-Baines. It takes you across the river
and back, with some beautiful sites of the many pinkish brick buildings the city is known for.

Then we headed out to [Cité de l'espace](https://en.wikipedia.org/wiki/Cit%C3%A9_de_l'espace), one of the main tourist
attractions in Toulouse. The highlight for me was probably the full-scale model of the Mir space station, which let
one walk through the station and see the interior. It's remarkable to me that Mir was operating starting in *1986*,
and some of the technology on display in the model seemed even older than that.

After lunch Hilary started to crash so we headed back to the hotel and I worked on the
{% include tag_link.html tag="supercollider" %} parser project for a bit. I've been communicating with another
SuperCollider developer some about the formatting project, and we've decided to decouple the SCLang code formatting
project from the current C++ work, which I think is prudent. It *also* means that this work is no longer on the critical
path, so that takes some of the pressure off.

Of course, I made a good step forward today when I realized that the parse tree has *cycles* in it, of all things, so
I refactored the C++ serialization code to uniquely number each ```PyrParseNode``` and then only refer to the nodes
referenced as subnodes by their index. I then pass an array of the nodes along. It's much quicker and the parse trees
have become a lot more tractable. In other words, despite the pressure being off I'm thinking I'll probably keep working
on this a bit more because it's pretty darn interesting.

I also started working on a simple HTML tool to allow me to click through the source code and see what nodes might be
impacted, or vise-versa with clicking on parse nodes and having them show what position they are in the source code.
It's a single page of HTML with some JavaScript, up to my usual level of JavaScript programming (which means it's
terrible). I know enough about JavaScript to know that you would never want to hire me as a JavaScript developer, it's
not a language that's designed to enforce best practices and I don't know very many of the best practices so what you
end up with is a mess. I'll probably link some example output here on my blog once it's presentable, and then point
folks on the PR for the parser too it, asking if they are interested.

We went out briefly for crepes for dinner, which were lovely. France is incredible but the language barrier continues
to be awkward. People in Toulouse are super nice and accomodating, the issue is just that I feel a little uncomfortable
interacting with folks because I know that expecting them to speak English is rude. I don't like being *that* American,
if you know what I mean.

Hilary is trying to sleep again so I'll probably keep this short.

