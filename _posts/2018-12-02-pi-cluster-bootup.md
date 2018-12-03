---
layout: post
title: "Pi Cluster Bootup"
date: 2018-12-02
tags: [ personal, sclork ]
---

Bruno has scheduled two SCLOrk hacking days for time to develop whatever code
we can in time for the semester to start, students to come onboard, and for
the recital we have booked in January. This was time I had booked off from work
anyway, so I was happy to plan on joining for both days. Given my recent
decision to develop my own network clock algorithm I made a goal today to try
and get to a place where the Raspberry Pi cluster I had been working is up
and running, with {% include tag_link.html tag="supercollider" %} built for
ARM and working, at least the language and the synth server.

So first thing was to dust off the Pi that I have hooked up to the touchscreen.
It had a 128 GB SD card sitting in it running `Gentoo`. I was working on a PXE
boot situation for the cluster but after digging a bit further on that I think
it would absolutely be the right idea for long-term maintenance of the cluster
but the documentation is scant, and it was starting to turn into a research
project of its own.

Given the time lines, I've ordered some of the Samsung 32 GB SD cards for each
Pi in the cluster. Next was to use tar to transfer the Gentoo system I have
working now to a 32 GB SD card, so that it's super easy to just use `dd` to
clone the image to the other 8 cards. Then it's just a simple modification of
a few things like the `hostname` file to make each one have a correct hostname
and we're good to go.

I got `dnsmasq` working with fixed IPs and hostname resolution, and got `pssh`
package installed and configured. Next up is checking out Supercollider so I
can get the synth building without X, because the Gentoo distro of SC is
configured to pull in X. If I can get SC built on this single Pi it will then
be able to come along for the ride when I clone the image.

Lots left to do, but it's time to head back to work tomorrow, so wrapping it up
for the night.

