---
layout: post
title: "Confab File Downloads"
date: 2019-07-31
tags: [ personal ]
---

So this morning's deep working session I was able to finish the file download portion of the
{% include tag_link.html tag="sclork" %} asset system. The Pistache library I'm using for both client and server sides
of the HTTP transfer part of Confab chokes when sending packets larger than 4K minus *some margin*, which this morning I
determined by binary search through powers of two to find the maximum packet size. Next up is the list system, starting
a new branch for that.

Not really a whole lot else of interest today so I'll leave it at that.

