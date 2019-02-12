---
layout: post
title: "SCLOrk Rehearsal with Pd"
date: 2019-02-11
tags: [ sclork ]
---

The folks outside of the normal {% include tag_link.html tag="sclork" %} class met tonight for the
fortnightly Chamber SCLOrk rehearsal. We were meeting every weeknight for the runup to the Public Domain
performance, but now it's back to once every two weeks. While I do appreciate having some Monday evenings
back to myself it was nice meeting every week to help keep SCLOrk top of mind.

In any event, Bruno had volunteered us to be the local chamber laptop orchestra for the upcoming
[Linux Audio Conference](http://lac.linuxaudio.org/2019/), which is taking place this year at Stanford.
We got one submission, which is a piece based on Pure Data, instead of our normal programming
language of {% include tag_link.html tag="supercollider" %}, and uses WiiMotes in a series of Tai Chi
moves for performance. It looks to be a really fun piece to perform, although tonight was mostly
just about getting the WiiMotes paired with our laptops and making sure the basics of the piece
were working as expected.

I *did* get a chance to update the server with some attempts at fixing the ghost client issue. Somehow,
for reasons I can't spot as obvious, there are chat clients that are seen lingering in the signed-in clients
list after users has signed out. I had spotted a few bugs in the connection cleanup code in both client and
server, but it still isn't clear to me how there might be usernames lingering in the chat window. So,
I added some code that will scrub the list of signed in users each time someone requests that list, which
happens right now on any chat sign-in.

Hopefully that will keep the ghosts away, at least for now.

I also forgot to add in the last [SCLOrkChat](https://github.com/lnihlen/SCLOrkChat) iteration the feature
where the version number of the Quark is available somehwere, either in the window header or perhaps
reported when the user types ```/help``` or perhaps even a new command like ```/info```. I also recorded
a few other small feature requests but honestly I think the next step is going to be to continue hacking
away on the [SCLOrkClock](https://github.com/lnihlen/SCLOrkClock) version 2, now with that stopgap
solution in place.

As always, plenty to do, but getting home shortly before 10 kind of limits the post-SCLOrk-rehearsal options
to "quickly put up a blog post and then get ready for bed." Which is officially the plan.
