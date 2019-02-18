---
layout: post
title: "Dead Cells"
date: 2019-02-17
tags: [ sclork, supercollider, oort_cloud egregious ]
---

Perf is upon us at work and I'm of course infected with a particular case of the
lazies. Good thing the Dead Cells videogame is available on Switch now. Played
a few hours of that today, interspersed with some additional coding work on
the [SCLOrkClock](https://github.com/lnihlen/SCLOrkClock) refactor. It's feeling
a bit better in progress, although I'm not certain when the next version will
be available.

I got more of the server-side code written, and got tempo changes working too.
Then I got stuck with scheduling future changes to the clock. The
```TempoClock``` API has a facility for scheduling a meter change at an upcoming
beat, or an upcoming time. This gets tricky with a distributed clock cohort,
but it might be better to schedule clock changes in advance, to better control
synchronization. Meaning that tempo or meter changes on a local clock scheduled
to happen *now* still need to propagate to all other clocks within the cohort,
so by scheduling things in advance avoids propagation delay.

If we restrict scheduling changes to only beat counts instead of seconds it
simplifies the design, and I can rationalize the idea that seconds doesn't make
as much sense on a distributed clock. The idea is that clients and server both
maintain a priority queue of scheduled changes for all clocks in the cohort, and
then implement those changes on the local clocks as scheduled. It did occur to
me that any future changes would need to be communicated to clients as they
join a cohort, so they can pick up all future changes as well. The server could
maintain the list of changes too, only dropping the old changes off when they
have passed.

On the client, I kind of think I might be able to schedule the changes on
each local clock instance. This also represents a shift to a world where every
client maintains a singleton of every clock cohort at all times. On the server,
I can't think of an obvious way to compute beat counts on the individual clock
cohorts without also instantiating local instances of the clock cohorts. That
may not be such a bad thing, just seems excessive. We'll keep chipping away.

There's a request for a {% include tag_link.html tag="sclork" %} clock UI,
possibly built into the chat. I'm also starting to think it might be useful for
continued development of the network clocks, allowing for an overview of all of
the clock states at once. But I'm thinking of re-organizing the SCLOrk
Quarks into only two, the core data structures in a
[SCLOrkCore](https://github.com/lnihlen/SCLOrkCore) quark, combining all of the
non-UI parts from the current Quarks into a single consolidated spot, and then
[SCLOrkUI](https://github.com/lnihlen/SCLOrkUI), with all the UI widgets,
including a tiling window manager with pre-configured window geometry. I would
do it one quark but some of the server code I'm running on a headless server,
and the UI code breaks the library when I try to compile it there.

I wish there was some support within the
{% include tag_link.html tag="supercollider" %} language for conditional
compilation, basically the ```sclang``` equivalent of ```#ifdef```. Then I
could coalesce everything into a single quark, with the UI stuff just walled
off behind some macros.

So today was the day what we had designated that
{% include tag_link.html tag="oort_cloud" %} was going to record that split
single. I had been worried that the band would just show up unannounced, or
text within an hour or so of their intended arrival, but I took the risk that
they were going to maintain the flake pattern of recent prior planning around
this recording, and I tore down the drum set I play for that band, to make
room for the {% include tag_link.html tag="egregious" %} gear. I didn't lay
any tracks down but I'm hoping that tomorrow, with the time off, I'll set up
the new gear and do some experimentation.

And I really think I'm getting close to beating Dead Cells.

