---
layout: post
title: "SCLOrk Rehearsal"
date: 2018-10-29
tags: [ sclork ]
---

Spent a few hours last night hacking to get the chat program for
{% include tag_link.html tag="sclork" %} working. I had taken the day off in
anticipation of returning from camping this morning, so I got to sleep in a bit
late, then spent time shuttling folks around, shuttling the dogs home from the
kennel, then over the hill to grab Hil (hah!), then celebratory Ethiopian lunch
with Hil, then home. I got about an hour to hack on the chat program, tried to
add the `BeaconClock` stuff that we had wanted to experiment with, then it was
off back over the hill for SCLOrk rehearsal.

Of course, the added `BeaconClock` stuff didn't work at all. That's what I get
from last minute hacking. But the router stuff I had set up worked well. The
laptops we use for SCLOrk don't seem to support a version of NFS new enough to
mount the share I had on the server. So distributing the chat program was fun.
I did forget to autoscroll the chat window to the bottom on the addition of new
text, so that's a quick fix.

Then we tried to get `BeaconClock` working with some shared laptop editing. I'm
going to spend some time working with the Pi cluster to see if I can get them
up and running to characterize the lag between the clusters. We could notice
obvious jitter between the laptops when trying ourselves.

Back to work tomorrow. Somehow, one day off sometimes is worse than none.
