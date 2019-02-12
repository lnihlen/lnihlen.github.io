---
layout: post
title: "More Pi Cluster Prep"
date: 2018-12-04
tags: [ personal, sclork ]
---

I still have the goal of having the Pi cluster ready for software development
when we do the {% include tag_link.html tag="sclork" %} hacking days. Given
our schedules for the next two weekends before those days I'm feeling the
pressure to get the system up.

I think the SD cards are arriving tomorrow, so I'm taking time tonight to try
and get the system image on the one 32 GB SD card I have as ready as possible
for the copy job. Big task for the night is to get
{% include tag_link.html tag="supercollider" %} building on the NFS mount
attached to the RPi, then I'll do a `make install` so that it gets installed
onto the system image.

I'm building on the main audio Linux server at the same time, to understand
what a headless SC build requires on a pretty much naked Gentoo system.
My `cmake` build command line looks like:

```
cmake -L -DCMAKE_BUILD_TYPE="Release" -DBUILD_TESTING=OFF -DSUPERNOVA=OFF -DNATIVE=ON -DSC_IDE=OFF -DSC_QT=OFF -DSC_ED=OFF -DSC_EL=OFF -DSC_VIM=OFF -DNO_X11=ON -DNO_AVAHI=ON ..
```

I didn't really have to install much to get this going on the Intel Linux
machine but the RPi seems like although I have `jack` in the `USE` flags that
didn't pull in `alsa` or `libsndfile` so the RPi is building those now, as well
as `jack-audio-connection-kit`, which is the oddly verbose package name by
Gentoo standards for JACK.

It's likely JACK won't build before bed but getting that going I think will be
the last system requirement step before attempting to build SC itself on the
RPi. I think reasonable exit criteria before starting to clone the system image
8 times is to have a `SinOsc.ar` rendering audio out of the Pi headphone jack.

Hopefully tomorrow night.

