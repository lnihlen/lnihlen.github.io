---
layout: post
title: "Command Period Survival"
date: 2018-11-25
tags: [ personal, sclork ]
---

Devoted probably too little time today to preparing for tomorrow's
{% include tag_link.html tag="sclork" %} rehearsal. But we did go get a
Christmas tree from a lot in Soquel, and I also hung some lights on the
exterior.

The goal was to have a `BeaconClock` built in to `SCLOrkChat` that somehow
survives the mighty Command-Period, which is the IDE built-in hotkey to stop all
clocks. After much tinkering I have converted my `Tasks` to `SkipJack` jobs,
which at least means my UI keeps updating after a hard stop.

But the `BeaconClock` freaks out after deletion, meaning that there are some
internal OSC function bindings in there that start periodically throwing
exceptions and wigging out as it is trying to inform previously deleted objects
of having received new packets.

The best I can hope for tomorrow is a stalemate where we can survive the command
period, we ask folks not to delete the chat window until done, and I work up a
patch for `BeaconClock` so that it can elegantly survive deletion.

Ah but we are returning to the land of never-enough-time, with a three week
stint starting tomorrow and not ending until holiday break.
