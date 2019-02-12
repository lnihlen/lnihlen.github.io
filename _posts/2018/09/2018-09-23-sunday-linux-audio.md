---
layout: post
date: 2018-09-23
title: "A Sunday spent on Linux Audio"
tags: [ personal ]
---

First thing was to get the Genelec monitors set up in the living room and then
plug them in to my Dangerous Music Source. Then I spent a minute trying to get
that device working on Gentoo over USB. Running `lsusb` the name isn't obvious,
but by process of elimination (literally running `lsusb` with it plugged in and
not plugged in and looking for the unique entry) I find the Dangerous Music
Source is showing up as:

```
Bus 003 Device 005: ID 20b1:2001 XMOS Ltd
```

I was glad to notice that I had already added both `ALSA` and `jack` to my
`USE` flags, meaning that I would be able to avoid a lengthy `emerge --newuse`
rebuild. However, my kernel config did not include support for USB audio
devices, so it was time for a kernel recompile. Bit spooky but it seemed like
the kernel went for full recompile, despite the fact that I had built this
kernel from source before on this machine. Maybe Gentoo is now cleaning up
those sources or something?

A reboot on the new kernel seems to have kept my old configuration, which IIRC
was really only different from stock with the addition of support for the
onboard ethernet controller. Then there was a minute of mucking about with
ALSA to make it choose the USB audio device as the default, and realizing that
it wasn't looking in `/etc/ALSA.conf` for configuration info but rather
`/etc/asound.conf`.

Then I was off to the races, at least for
[Play Music](https://play.google.com/music) on Chrome. Of course,
{% include tag_link.html tag="supercollider" %} is going to take a bit more
work. First was a reboot after adding my user to the `realtime` group. Then
some faffing about with `.jackdrc` to get it to use the X20 as the default
ALSA device, which is causing confusion in sc because the Source doesn't have
any audio inputs, only outputs. That got me to a place where if I kick off my
own instance of `jackd` I can get sc to render audio, but if I'm relying on
sc to boot its own instance, which I prefer, it won't boot correctly. There's
also the issue of the `jackd` server not allowing other programs to access the
audio hardware while it is running.

I see some notes from various sources about how to use the jack ALSA plugin
which, IIUC, gets ALSA to render audio to jack. Then I suppose jack could be
configured to the actual audio hardware. Perhaps a user-specific ALSA config
could choose the ALSA jack plugin. Then jack could be configured to run on
user login. Maybe worth a try, next time I feel like messing with this. So
probably, like, later today.

We're trying out Hulu Plus, and I notice there's a new season of
[Samurai Jack](https://en.wikipedia.org/wiki/Samurai_Jack) out, so that's taking
some time too.

I found
[this article](https://dwnomad.com/2016/11/ditch-pulseaudio-use-an-alsa-looback-with-jack-fixed/)
which has cut down some of the extra stuff in
[this more detailed article](https://alsa.opensrc.org/Jack_and_Loopback_device_as_Alsa-to-Jack_bridge)
talking about how to use the ALSA loopback adapter to have ALSA render to jack.
Another reboot to add the ALSA Loopback adapter support into the kernel, becasue
I never feel like messing with modules for things that are going to be loaded
at all times while I'm using the computer, and don't have any concerns about
contamination of the GPL status of the kernel.

But besides figuring out how to get `jackd` to start on login, so Supercollider
is happily booting `scsynth` and rendering audio, I can't get Chrome to render
one byte of PCM to the ALSA bridge. Googling around, it seems like I might
have better chances with Pulseaudio. So, added it to the `USE` flags and am
now recompiling a bunch of fun components, namely the `qtwebengine` stuff
that is a new supercollider dependency, that pulls in Chromium.

So yeah, was building somewhere around 14000 of the 17000+ files of Chromium
when I went to bed.
