---
layout: post
title: "Bringing SCLOrk Home"
date: 2019-01-22
tags: [ personal, sclork ]
---

Limited time today to hack on {% include tag_link.html tag="sclork" %} but after
getting home I did manage to bang out the "return trip" in the round-trip
engineering project for our PublicDomain piece. Yesterday I got the
code-to-UI path working, where we parse the provided code into individual labels
and editable UI elements, but wasn't able to complete the UI-to-code path, where
editing individual UI elements will efficiently update the code. The keyword
there is "efficiently," in that as code gets longer doing the easy thing of
parsing the entire code string again becomes quickly intractable.

Fortunately, for the ```Pbindef``` statements in question for this UI, they are
quite tractable, with none of them over 100 lines. So, with cutting a lot of
corners, we can make the computer work a bit harder in order to make it possible
for me to complete workable solutions in a relatively short time.

While a lot of what I've built for SCLOrk feels like infrastructure, meaning
that typically those pieces will be used for every rehearsal and performance
that we will do, the [SCLOrkPD](https://github.com/lnihlen/SCLOrkPD) Quark is
obviously designed for a single-use piece. After the end of the month, where
we are planning on performing the PublicDomain piece, I'm not sure we'll ever
want to use this again.

So the tight timelines are probably also good because they bound the time I'll
spend on this project. But I'm quite enjoying myself, for the time being.
A brief but intense engagement, as it were. Although these things do have a
way of coming back time and again. We shall see.

