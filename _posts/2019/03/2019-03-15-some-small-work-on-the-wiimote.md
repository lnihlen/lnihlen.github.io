---
layout: post
title: "Some Small Work on the Wiimote"
date: 2019-03-15
tags: [ personal, sclork ]
---

After work and dinner with Hilary there was a bit of time to sit on the couch,
with the latest episode of RuPaul's Drag Race on the TV, and hack a bit on the
Wiimote interface for {% include tag_link.html tag="sclork" %}.

I've been following along with this
[homebrew documentation](https://wiibrew.org/wiki/Wiimote), although translating
it to follow the conventions of the SuperCollider
[HID](http://doc.sccode.org/Classes/HID.html) interface has taken quite a bit
of experimentation. If I had to guess, I think the HID classes were designed
with devices that send a fixed pattern of bytes, either periodically or
asynchronously back to the host. If that were the case with the Wiimote, I think
using the HID classes would be super easy and slick.

The challenge here is that the Wiimote can be configured to communicate in a
variety of different ways with the host, and seems like it was mostly optimized
to minimize battery consumption except for when needed. All that said, I've
been able to get communication working at least somewhat reliably for everything
but the accelerometer. I think that's coming through, and finally decided
tonight to just send the data to control bus on SuperCollider. The Wiimote
is sending the data at 200 Hz or so, so calling back a function, like what I'm
doing with the buttons, seems a bit excessive. Dropping the data on to a bus
means everyone, both client and server, can access the latest data with
minimal latency.

So I'll be building that shortly. Assuming I can get some time to tinker this
weekend. It's kinda the last heavy perf weekend, so lots of homework. And I
think I'm coming down with a cold or something. Feeling super run down. But
seeing accelerometer data from the Wiimote light up a
[ScopeView](http://doc.sccode.org/Classes/ScopeView.html) would honestly make
my weekend.

