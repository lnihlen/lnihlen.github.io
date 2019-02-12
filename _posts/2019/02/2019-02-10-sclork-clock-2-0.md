---
layout: post
title: "SCLOrkClock 2.0"
date: 2019-02-10
tags: [ sclork ]
---

With the next {% include tag_link.html tag="sclork" %} recital tomorrow night I
had set a deadline to try and get a new version of
[SCLOrkClock](https://github.com/lnihlen/SCLOrkClock) up and running. The first
version, while surviving a live performance, did not support tempo changes,
which I try not to think about too much or I will start to become somewhat
embarrassed, particularly since I bumped the version number on the Clock to 1.0
after the first live performance.

Ah, well, so although I did bang out a bunch of code today it really was
starting to feel like I was headed down the wrong path. After letting the clock
sit for a few weeks while I took the time to hack out a prototype of
the [SCLOrkPD](https://github.com/lnihlen/SCLOrkPD) piece I think the design
of the clock had melted a bit in my brain. The half-completed design doc I
had written didn't reflect the thinking I had done about the clock in the
interim.

So I modified the doc a bit and started hacking up a set of client/server
objects for a new clock design. But this afternoon I had to conclude that I
had probably headed down a wrong path. The clock design just wasn't coming
together, and certain compromises I had to make left the system feeling
inelegant and brittle. That is not good for network distributed code, in
particular.

To buy myself a bit of breathing room I've pushed v1.0.1, which allows for
a non-default tempo on the construction of the clock, but not changing it
thereafter. This should, at least, unblock the students in the SCLOrk class
and allow them to finish their project with a bit more expressive range.

I think I've reached a good middle ground in my design, where "clock cohorts,"
a term I'm using to describe a set of clocks identified by a shared name and
locked to a tempo, also share a beat count based on a server-normalized start
time. This avoids a lot of the added complexity of allowing each distributed
clock in the cohort to have its own beat count. It also keeps a lot of the
flexibility of being able to create an arbitrary number of clocks within each
cohort, and an arbitrary number of cohorts (within reason, natch) on the
network.

One lesson learned from this first semester run of SCLOrk code is that there
needs to be ways to clean up state. So any clock within the cohort that calls
```~clock.stop``` should stop every clock in the cohort and delete the cohort
name. Otherwise it's likely they'll be a couple dozen stale cohorts running
around and students appending ```-new``` or other horrible things like that to
their cohort names.

Long week in front of me so heading to bed reasonably soon. Dark Sky is telling
me I might get a day or two of respite from the rains, but I'm not feeling
super confident. This may be another week of pickup truck rides over the hill
and back.

