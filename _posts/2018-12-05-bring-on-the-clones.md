---
layout: post
title: "Bring on the Clones"
date: 2018-12-05
tags: [ personal, sclork ]
---

I kicked off the compile of {% include tag_link.html tag="supercollider" %}
targets `sclang` and `scsynth` last night before bed, so when I woke up this
morning I had just enough time to check that the build had completed without
error before heading off to work. Worked all day, and was stoked to get the
notification on my phone that I had received delivery of the SD cards.

So, after verifying the Supercollider build on the Pi with the classic

```
{ SinOsc.ar }.play
```

I shut it down and copied the 32 GB disk image to the server using a USB SD card
reader. Then I started using the reader to clone a copy of the disk image but
it is taking *forever.* I noticed that each of the SD cards I got came with a
USB dongle-looking thing which turns out to be a SD card adapter.

So now I have every USB port on the server occupied with one of the USB adapters
busily cranking out a copy of the SD card image. I'm not timing it but I think
I'm at least a half hour into the writing of the first SD card so I it's
going to be a little while, but at least 6 writes are happening in parallel. Of
course, since the first copy hasn't completed I haven't had the opportunity to
*verify* the copy of the image works, but hopefully I'll see soon. Given that
the usage of each of these images is substantially less than 32 GB it might
make more sense, if I have to do the copy again, to write a script that makes
the filesystem on each drive using `fdisk`, then just extract the filesystem
to each partition.

Next step will be to individually bring up each Pi in the cluster, setting up
hostname and IP address, then dropping it on to the network. Given that we're
now an hour in to starting the first copy, with no end in sight, it's already
becoming pretty obvious why folks would want to do this with PXE boot and NFS
mounted drives.

Of course, I also haven't given much thought to the algorithm I want to try
and implement for the centralized clock testing. I also want to get the
server-based recording working, and there's some automated analysis that I
could also work on. I'm starting to feel that the buildout of the development
environment is probably looking to be a lot more work than the actual
development of the software. But I'm having fun, and it's got a lot of
interesting challenges - building a small cluster, working on Gentoo on ARM,
automated analysis of multichannel audio files, Linux networking, distributed
audio programming, etc. Lots to learn and do!

