---
layout: post
title: "Incremental"
date: 2019-02-24
tags: [ personal, kfjc, egregious, sclork ]
---

It was a day for small steps on a variety of projects. I worked some more on
the office space, combing through a ton of detritus in order to make room for
additional equipment. I'm expecting some power conditioners tomorrow for the
rack space I have, so I can set up the couple pieces of equipment I have that
have been sitting around waiting for rack space. I managed to find a set of
rack mount brackets for the Nakamichi tape deck with balanced outs that has
been sitting in my closet for a long time.

So there's definitely a lot of good noise work happening on cassette these days,
and I'm stoked to get a proper cassette deck going. There's a long line of
releases queued up, and I'll be glad to let the music department at
{% include tag_link.html tag="kfjc" %} know that I can handle cassette
reviews again.

Spent a good amount of time on the {% include tag_link.html tag="sclork" %}
clock v2 refactor, and managed to get the network clock synchronization back
working again. Given that was a basic feature of the first version of the clock,
it seemed to me sort of unfortunate that the fancy new version, despite
supporting many new features, should not be able to do the basic thing of being
a synchronized network timekeeper as well as the original.

So it was good to see the beat count turning over at (roughly) the same time on
both my desktop and laptop. Then I got the upcoming change scheduling working,
so it is now perfectly reasonable to lay out all of the tempo changes in a
score in advance, or set them as you go.

The ```bar``` and ```beatsPerBar``` parts of the clock are probably still
pretty buggy, but follow in the same pattern as the tempo changes, so *should*
flow pretty naturally in as they are needed. But it seemed higher priority to
build a handy-dandy UI to show all current clock states, their tempii, and have
a built-in flasher for each clock, so I built that next.

I'd say that is the goal of having the clock working for tomorrow's SCLOrk
rehearsal fairly well met. Given we are performing on Wednesday I don't think
it would be prudent to bring in the new stuff tomorrow night anyway, but things
are now in a form where I can show progress and get some feedback. I'll be
meeting with Bruno tomorrow for an early dinner before rehearsal, so looking
forward to talking through the clock, and some upcoming changes I have in mind
for the rest of the code base, then.

There was also some work stuff to get through, and additional prep work for
the coming tax season. I have a long list of paperwork to scan and upload.
So yeah, things getting better here and there, but no satisfying conclusion
of really anything.

I've been feeling the call of some of the more neglected projects starved for
cycles right now, particularly that of {% include tag_link.html tag="vcsmc" %}
and {% include tag_link.html tag="scintillator" %}. With Hilary heading out
of town for a week in April I'm half inclined to take the week off and just
sit at home, hacking away on these things.

We'll see as we get closer. Taking time off from work to work is a habit that
is perhaps not wise to cultivate. But I want what I want. What I decide to do
about it is where the free will comes in.

