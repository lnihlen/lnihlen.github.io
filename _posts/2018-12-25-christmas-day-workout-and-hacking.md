---
layout: post
title: "Christmas Day Workout and Hacking"
date: 2018-12-25
tags: [ personal, vegan, sclork ]
---

When I was a kid I remember my mom setting an early morning limit, a time before
which I was not to disturb others in the house on Christmas day. This was, of
course, to prevent me waking my parents up before dawn.

Of course, now as an adult in a white-collar job with Christmas day off, we
once again slept in, then had leftover {% include tag_link.html tag="vegan" %}
cranberry pie for breakfast along with some coffee. Sometimes being a grownup
can be pretty cool.

Hilary and I exchanged gifts, she got me a second pizza stone that will fit in
the oven, along with a pizza throw so I can actually hope to deliver the pizza
to the stone and retrieve it once its prepared. She also got me some awesome
binaural field recording microphones which I'm planning to experiment with soon.

I did my usual strength training routine for a Tuesday, but at a comfortable
12:30 pm instead of the traditional workday time of 6:30 am. After polishing
off a few more chores it was time to shower and change into pyjamas, with the
intention of spending the rest of the day on the couch watching movies with
Hilary, cuddling with the dogs, and hacking on
{% include tag_link.html tag="sclork" %} code.

And that's exactly what happened. I made substantial progress on the
[SCLOrkChat Quark](https://github.com/lnihlen/SCLOrkChat), adding a selector
for message type, rendering for code message types, the list of signed in peers,
more detailed test code, system messaging to the chat view, as well as some
other forms of UI polish.

Big work items left:

  * Some way to copy code messages into the GUI paste buffer.
  * Selected targeting of users for private messages.
  * Nickname changes.
  * Timeout of unresponsive clients.
  * Director mode, which adds a "shout" option to the message types.
  * Finish documentation and package Quark into first release.

I'm hopeful this will all work out in the next day or two at most, but it is
quite a bit of work. Should be lots of fun, however!

