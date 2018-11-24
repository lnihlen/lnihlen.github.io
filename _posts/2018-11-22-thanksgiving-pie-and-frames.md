---
layout: post
title: "Thanksgiving Pie and Frames"
date: 2018-11-22
tags: [ personal, vegan, vcsmc ]
---

The pecan pie I made last night set in the refrigerator as best it could, and
I was able to cut a slice this morning to enjoy with my morning coffee. So,
breakfast mission accomplished. I noticed that the space left by the piece of
pie quickly filled with goo from the other pieces. As it's my first pecan pie
from scratch I'm not sure if it's some failing on my technique or a failure of
the recipe to have found a reliable {% include tag_link.html tag="vegan" %}
binding agent that is as effective as eggs. Still, it was tasty. I might try
the same recipe next time but try to find some of the prepared egg alternatives.

Had some time then to focus on {% include tag_link.html tag="vcsmc" %}. Working
with video is a lot of fun. I got to a place where I was getting some image
output from the `split` program I wrote, which decodes individual frames and
outputs them as pngs. However, the colors were out of order. So, I found myself
making a classic test image, with memories of prior work on video pipelines
echoing in my head:

![rgb test image]({{ "assets/img/blog/2018-11-22-1.png" | absolute_url }})

Then it was a simple matter of swapping the color channels in `libav` around
until the colors match the labels. There's still a segfault on closing the file,
and the API around end-of-file detection is sorta awkward, with the
`GetNextFrame()` function returning `nullptr` and then requiring the caller to
call another function to determine end of file status. But it feels good to see
frames coming out of my own code.

I also got a chance to make another pie-related food for the Thanksgiving
festivities. I made the Seitan Pot Pie from the classic vegan cookbook
Veganomicon. So, dinner was pot pie followed by pecan pie for dessert.

All in all, a pretty damn good Thanksgiving.

