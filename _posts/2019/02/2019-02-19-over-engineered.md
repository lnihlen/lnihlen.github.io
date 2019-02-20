---
layout: post
title: "Over-Engineered"
date: 2019-02-19
tags: [ sclork ]
---

Beating Dead Cells definitely cleared up a few hours of free time in my schedule
per day. So I used the time to get started on some additional furniture for
the studio office, and make some additional headway on the network clock
refactor for {% include tag_link.html tag="sclork" %}.

So the latest shoals for my design boat to founder upon has been trying to
figure out how to allow for distributed changes to clock cohorts in a clear way
that doesn't melt my brain. So midway through designing a custom data structure
to hold both current clock state and upcoming states in a priority queue, as
well as all local clocks now having two scheduler queues, one for clock events
and one for clock state changes, I'm starting to wonder if perhaps the clock
is over-engineered.

Flashback to what I usually call *the troubles*, the period of time right before
I moved out to California and joined Google. The short version of this is that
many fundamental elements of my personal and professional life went into the
emotional equivalent of a chipper shredder.

In any event, I remember on more than one occasion going to the local BMW
Motorcycle dealership to admire the BMW GSA motorcycles. This is a motorcycle
that people routinely choose to drive around the world. I did end up getting
one of these fine motorcycles, after about a year of work here at the Googe.
It's a bike that a lot of engineers tend to gravitate to, I've noticed. It
does have a reputation, according to some, of being "over-engineered."

There's a discipline to thinking about things in depth, refining them again and
again, trying to make the most well-designed object possible. It's possible that
the clock I'm designing is over-engineered. And "perfect is the enemy of the
good" is a real problem in software development that I've seen personally
derail teams and projects.

On the other hand, I'm proud to recall that our first live performance of
SCLOrk based on the software that I built had no issues. So maybe the code I
write sometimes requires me to struggle through the occasional subtle design
issue that, if I build it right, will *just work* for people using it. And
maybe it takes longer to get to the next production version than I would like.

But what I'm building would hopefully take you around the world and back again
without complaint.

