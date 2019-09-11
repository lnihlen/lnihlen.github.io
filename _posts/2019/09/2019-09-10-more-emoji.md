---
layout: post
title: "More Emoji"
date: 2019-09-10
tags: [ personal ]
---

So it was a long day of training but then it was home and some time to work on improving the emoji support in the chat
program for {% include tag_link.html tag="sclork" %}. It seems that the Ubuntu distro on the orchestra computers needs
to be explicitly told to use a color emoji font, even with it installed, otherwise it falls back to the black-and-white
emoji, with very limited coverage.

If I explicitly set the font to something robust, like Noto Color Emoji, then the emoji render in color and with great
coverage, but non-emoji characters render in kind of an awkward font. So tonight I spent some time trying to see if I
could coerce the Qt controls inside of SuperCollider to mix fonts, with no real success. This means I'm going to have to
spend a bit of time redesigning things, like making the text entry box not render emoji, and the chat messages send the
descriptions instead of the raw emoji, so that the they can be rendered in a separate view. A bit more of a mess but in
the end we'll have full-color emoji, and can perhaps even scale them differently in situations of sending only a few
emoji, kind of like how the iPhone does it in messages.

I didn't make it far, but I think the path forward is starting to become apparent.

