---
layout: post
title: "Grind Phase"
date: 2019-08-07
tags: [ personal, sclork ]
---

I spent this morning's deep working session rounding out some of the parts of the list feature for the asset sharing
system in Confab. It's in that phase of the work where I've wired up all the libraries, learned some of the interesting
bits and now it's mostly just execution, so it's feeling like a bit of a grind.

There was some discussion on the SuperCollider user group about adding a HTTP library to the SuperCollider language,
which made me wonder if I could refactor the client part of the C++ code inside of Confab to be a pure OSC to HTTP
proxy. However, after consideration, I think this more customized approach is more suitable for our situation.

I think that SuperCollider has a wonderful extension system with Quarks, with a convenient built-in system for adding
new SC classes and documentation, as well as version control and updates. Where things get messier, however, is when you
start wanting to add C/C++ extensions to the language. Right now there really isn't any way to do that without modifying
the SC code base itself, which obviously doesn't scale or ship outside of one's own project. Worth putting on the list
of things to think about for the language.

I'm in that phase of my XCOM2 game where a series of unlocked missions is all that separates me from the endgame
content. But, I want to unlock all the fun endgame toys, like the plasma machine gun and shotgun, powered armor, and the
remaining chosen assassin weapons. So I'm waiting around while the cash piles up, trying to find ways to accelerate the
final research and production projects. It's a good place to be, I guess, in terms of the likelihood of success of this
game, but it's making me feel like that I either made some very poor choices on my tech tree or the timing of the game
is now a bit lopsided with all the DLC. It's still fun, just awkward. Art imitating life?

