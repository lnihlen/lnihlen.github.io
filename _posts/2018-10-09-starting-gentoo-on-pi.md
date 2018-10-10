---
layout: post
title: "Starting Gentoo on a Raspberry Pi"
date: 2018-10-09
tags: [ personal, sclork ]
---

So Bruno, fearless leader of {% include tag_link.html tag="sclork" %}, wanted
some of us to look in to the
[Utopia Quark](https://github.com/muellmusik/Utopia), which is being developed
for network synchronization of
{% include tag_link.html tag="supercollider" %} music programming. So it may
have not been the most productive direction to pursue but I ended up tinkering
with putting Gentoo on a Raspberry Pi. I got as far as hand-optimizing the
microSD card geometry, then making the file system.

There's [a page](https://wiki.gentoo.org/wiki/Raspberry_Pi) on the Gentoo wiki
with some loose guides. No AMD32 handbook, unlike the myriad other architectures
that have one on offer. Thinking like I'm heading into the hinterlands here, and
that isn't the point of the exercise. So, I'll probably just end up putting
NOOBS back on this SD card, or perhaps just a regular Rasbian distro.

Time to focus on an actual plan for testing out some of the `BeaconClock` stuff
in Utopia. Something like:

  1. Get a usable Raspberry Pi Linux distro installed on the new SD card that is
  supposedly much faster than the one that came from stock.
  2. Setup `dnsmasq` on the Pi, with configuration so that my laptop can get
  a static IP address on an ethernet network connection to the Pi.
  3. Experiment with Utopia on a 2-computer network, using the Pi as a server.
  4. Use a multi-track recorder to measure synchronization between the two
  computers, each issuing a simple pulse to the audio output on receipt of the
  broadcast ping.
  5. I had ordered a
  [fanless rackmount computer](https://www.logicsupply.com/products/rackmount-computers/fanless-rackmounts/)
  for the audio rack that I have, but it's a custom build from Logic Supply so
  that might take a minute. That will ultimately take the role of server in this
  setup, with the Pi standing in as a client Linux computer, perhaps ultimately
  to be replaced by the set of SCLOrk laptops we use for live performance.
  6. Once that arrives and is configured, explore other use cases for that
  hardware. One thing that immediately comes to mind is multi channel recording,
  perhaps with an automated start/stop one-touch kind of button setup, although
  knowing levels would probably be pretty important there. We shall see.

For SCLork, I could see such a server having many uses, besides the above
mentioned two of making a recording of our live performances and being a
synchronization clock source. In our last gig we used a spotty internet
connection to connect to a group chat on IRC. I think a local IRC host, with
everybody having hard-coded IPs, could make for a much more reliable and secure
means of tying the group together. Plus lots of other ideas begin to form,
such as the possibility of allowing folks to share more than just text,
including code snippets and even bits of rendered audio.

So I'll have to hold my nose and dive into another Linux distro, saving the
uphill climb of Gentoo on a Pi for much later.
