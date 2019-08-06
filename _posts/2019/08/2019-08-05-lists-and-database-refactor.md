---
layout: post
title: "Lists and Database Refactor"
date: 2019-08-05
tags: [ personal, sclork ]
---

The goal for this morning's deep working session was to make substantive progress on the list feature for the confab
database for {% include tag_link.html tag="sclork" %}. But I had all of the LevelDB Database stuff abstracted away in a
separate class from the logic around accessing things like Assets and Lists, and it wasn't working any more to build an
increasingly sophisticated Database abstraction layer for *one other consumer* in the code.

In fact, I think there's a great many things that are starting to pile up that I'd like to refactor and reorganize, but
I'm pushing to complete this first round of features and get something out of the door before I start rewriting the
whole thing from scratch again.

The rest of the day was fairly routine, work followed by leftovers at home, then some XCOM 2 where I took down that
second Chosen, this time the Warlock. And then it was time for bed.

