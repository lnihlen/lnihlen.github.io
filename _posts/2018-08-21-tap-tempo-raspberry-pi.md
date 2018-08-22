---
layout: post
title: "Setting up the Raspberry Pi for Supercollider"
date: 2018-08-21
tags: [ supercollider, i_made_a_thing ]
---

Set up the Pi last night, these things are surprisingly quick for being
comparatively inexpensive! Now working to follow the
[instructions](https://supercollider.github.io/development/building-raspberrypi)
for building from source.

First is getting
[rasbian stretch](https://www.raspberrypi.org/downloads/raspbian/)
going on the Pi. Since I couldn't get the plastic sd card insert I had put in
my laptop out of the SD slot I went with the NOOBS option. Rasbian stretch
was the first option on the list after getting the device connected to WiFi so
this took no real effort to get going, only the wait for the download and
install.

Not super jazzed about all the random extra stuff on the OS image that I'm
waiting on during the install process. But I'm impressed with the "batteries
included" vibe of the Pi, and I suppose if I wanted to trim the distro down I
shouldn't be following the NOOBS process but should rather pursue an install
of my favorite distro [Gentoo](http://gentoo.org).

Meanwhile Hil and I are watching [Faster](https://www.imdb.com/title/tt1433108/)
in our ongoing project to watch every
[Dwayne Johnson](https://en.wikipedia.org/wiki/Dwayne_Johnson_filmography)
movie from oldest to newest. Some of them have been real stinkers, but this one
ain't too bad. Hilary said it was "the longest episode of Law and Order" ever.

The quad cores make a big difference in the Raspberry Pi but when something
is single-threaded you can tell that those threads aren't spinning around too
fast - the UI remains responsive because there are three other cores waiting on
the input but batch processes take *forever* on this thing.

.. And I ran out of time. I only get maybe an hour of so of free time on most
weeknights so progress is always little drips and drabs. The life of an
intrepid engineering manager.
