---
layout: post
title: "SCLOrk Startup"
date: 2019-09-09
tags: [ personal, sclork ]
---

After a relatively chill return to work I got to attend the first {% include tag_link.html tag="sclork" %} rehearsal of
the season. It was good to see everyone after the break, and even though I hadn't completed much of what I had set out
to do all we really needed was the chat program, which was mostly working, so at least we weren't blocked.

I had some issues getting the emoji feature I had built into the chat to work correctly. The emoji are showing up black
and white instead of color, with the vast majority of them missing and rendering as empty boxes. A little Googling
around and I think we could solve the issue by specifying a particular emoji font, probably "Noto Color Emoji," when
rendering the individual emoji characters. It's going to be a bit of work to break out particular characters for
rendering in a different font, but I kind of wanted to put them there anyway, to support a tool tip. So that could be a
short patch project.

We also uncovered a few minor bugs in the distributed clock, and I made a few more notes about improvements, and then we
worked on a piece proposed by one of the members. It was great to be back in the saddle making sounds with the group.
Looking forward to the next rehearsal in two weeks.

