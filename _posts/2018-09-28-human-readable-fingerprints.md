---
layout: post
title: "Human-Readable Fingerprints in vcsmc"
date: 2018-09-28
tags: [ vcsmc ]
---

Well another work week gone,
[Fate of the Furious](https://en.wikipedia.org/wiki/The_Fate_of_the_Furious) on
the TV, and I'm noodling with some sort of human-readable fingerprint name
system for vcsmc. This is a completely ridiculous fluff feature for those
end-of-week moments when my brain feels like roughly the consistency and worth of
Cleveland road ice in early spring (dirty slush). Why get excited for names like
`0xe03778443080da82` when there could be something cool like
`CritiquedAllograftSchizaxonUnflouted`?

A bit of Googling uncovered
[https://github.com/dwyl/english-words](https://github.com/dwyl/english-words),
which I quickly added as a submodule. The `words_alpha.txt` file has 370098
words in it. So I've started in on a simple bit of code that will load that
file, parse in each line to a string in a giant vector, and capitalize each
first letter in each string while doing so.

Then, a 64-bit number gets translated to base-370098 number, where each digit
is an index into the giant string table. The resulting ID string is just a
concatenization of each "digit" with a capital letter at the start of the
string. And then we have a human-readable string, albeit a completely
nonsensical one.

I'm wanting to build a bunch of logging stuff, with fun features on html pages
explaining the ins and out of the evolutionary programming process, so this
was a fun feature to bang out in an hour or so.

