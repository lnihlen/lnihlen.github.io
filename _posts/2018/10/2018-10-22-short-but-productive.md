---
layout: post
title: "A Short But Productive Evening with Utopia"
date: 2018-10-22
tags: [ sclork ]
---

Had a short but productive evening hacking on the fanless server (named
`cooper` in honor of the Twin Peaks rewatch). First I fixed the packet
forwarding on `cooper` by enabling it in `/etc/sysctl.conf`. I had completely
forgotten that it is turned off by default in this file, and the various
tutorials and documentation I had been reading about this didn't mention it.
There was one vague hint about setting the `/proc/sys/net/ipv4/ip_forward`
status to `1`, to "enable packet forwarding," but this of course does not
persist between reboots, as it is sourced from the `sysctl.conf` file on bootup.

Once that was set up I had packet flow, with my laptop able to connect to the
Internet via an IP address assigned to it by `cooper`, and treating `cooper` as
the gateway. Only took me an hour to figure that one out.

In a fitting parallel, Agent Cooper just got his conciousness delivered back
to him, after electrocuting himself as Dougie Jones, during this rewatch of
Twin Peaks.

Next was more faffing about with the Utopia quark. I had noticed a while back
that when both my desktop and laptop try to connect to the same `Hail` instance
the second computer to connect will start to tightloop on reconnect attempts.
The `Hail` object sources the client name from a local invocation of `whoami`,
and since I use the same username on both computers it is causing duplicate
`Peer` name issues.

So this evening I spent some time trying to write a short loop that would append
`#n` to usernames supplied to the `Hail` in order to prevent the duplicate name
tightloop. But, I ran into an issue, which is that I need to join the `Hail`
before I can determine what names are already in use in that system. The
discovery moment is that `Hail` is a *decentralized* discovery system, so there
would need to be some exterior way of guaranteeing unique names in order for
everything to work.

It occurs to me that I'm already running a server, so relying on a decentralized
system for peer discovery is adding needless complexity. There may have been an
aesthetic sensibility here, perhaps Bruno would like to say proudly that we are
avoiding patriarchal patterns of centralized control. But in the interest of
utility and efficiency, for now I will assume that having a Central Scrutinizer
is tolerable. Time to start exploring the `Registrar` family of classes in
Utopia.

For another night.
