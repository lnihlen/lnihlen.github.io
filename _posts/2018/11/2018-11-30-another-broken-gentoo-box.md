---
layout: post
tite: "Another Broken Gentoo Box"
date: 2018-11-30
tags: [ personal ]
---

We've had intermittent power failures here thanks to the constant rain of the
last week. As a result this morning the computer I use as a router and DHCP
server was acting up, and the Internet connectivity was flaky.

It got worse after I left work, so I texted Hil a reminder on how to power cycle
it, which seemed to resolve the problem. I picked up a new UPS at Fry's on the
way home, hopefully that will help the setup through troubled electrical waters.

However when I got home I noticed the Gentoo workstation I've been using in the
living room has taken a turn for the worse, with the NIC unable to get an IP
address despite every other device on the 'net being happy. Restarting the
network only reminded me that I had configured it to not mount the NVMe drive
I have for `/home` until after bootup by marking it as a network drive, because
the machine promptly tried to unmount `/home` before restarting the network
services, and then hardlocked. Rough. After a reboot/fsck/reboot cycle I
thought I'd take a stab at fixing that first, and set up a `/etc/local.d/`
script to mount `/home/`. And, of course, forgot to `chmod +x` it, so on reboot
I was left with a machine that wouldn't let me log in because it can't find
my home directory.

And, of course, because it still can't seem to get a network address, I can't
`ssh` in to it either to try and unscrew it from my laptop. Next recourse is
to boot it off a Gentoo system image, `chroot` in to it, and try again.

So now instead of one problem (no net) I have three. All in all, a productive
Friday evening.

