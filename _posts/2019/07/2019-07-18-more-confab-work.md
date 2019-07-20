---
layout: post
title: "More Confab Work"
date: 2019-07-18
tags: [ personal, sclork ]
---

So I took several long breaks today to rest but also managed to really dig in some on Confab, the asset sharing system
I'm building for {% include tag_link.html tag="sclork" %}. I built a couple of HTTP endpoints out using Pistache and
tested them using curl. I can store and retrieve Assets with inline data from HTTP. Not bad for a days work, and while
recovering from surgery to boot.

I'm thinking of two new features that might have to be included in the minimum viable set - automatically collected
lists of Assets, which are maybe more of a tagging sort of thing, and also named references to assets, so not everyone
has to remember a bunch of 16-digit hexadecimal strings in order to access their data. I think some of these feature
ideas are coming from implementation needs of the system itself, and some are coming from thinking through how I want
the overall end user experience to work. It might make sense to list them out a bit more and analyze from there. But
then that causes me to redesign a bunch more of the code I've already written for SCLOrk based on this, and all the
requirements start getting super fluid and... that's when I take a rest.

Day by day I'm getting stronger, but still not back to 100% yet. Good thing I have tomorrow and the weekend before I'm
required to be smart to make a living.

