---
layout: post
title: "Wiimote on HID"
date: 2019-03-09
tags: [ personal, sclork, supercollider, scintillator ]
---

Although it probably wasn't prudent I decided to take a day off from work and
play around with some code for {% include tag_link.html tag="sclork" %}.
Actually the morning didn't start out with that plan. I had re-installed
Dwarf Fortress last night with the intention of starting a new fortress
project this morning.

I think DF these days is too much like work. I've always had a pet theory that
managing at Google is a lot like playing a Dwarf Fortress game. Substitute the
booze in the game for coffee at work and there's actually a surprising number
of parallels. Fun to think about, but when I'm looking for a break from work
perhaps DF might not be the best option.

Sharing this with Hilary later and she was completely unsurprised. She says
that nowadays the only time I play DF is during a long vacation. I find it
interesting when I discover something about myself that is completely obvious
to Hil. It happens fairly often.

What did grab hold of me was starting to make further effort on the C++ code
for the Wiimote interface. I made some progress on that, enough that I decided
it was time to start working up the bridge code on the
{% include tag_link.html tag="supercollider" %} side. Turns out, there's a whole
```HID``` interface in SuperCollider, and it uses ```hidraw``` on Linux. So,
the C++ program was instantly rendered redundant. The afternoon and evening
I spent trying to reconcile some of the existing documentation around the
Wiimote and its communication protocol with the HID documentation in
SuperCollider.

I was able to get button and even accelerometer readings working, although the
latter came online only right towards the end of the evening and frankly were
a bit rough. I had hoped that the firmware on the Wiimote was calculating
the accelerometer data into roll and pitch values for the Wiimote based on
gravity's downward acceleration but that is not the case. The acceleromter data
is raw off the sensor, or feels that way. So tomorrow I'm going to spend some
time figuring how to get higher-quality data from the sensors, as some of the
least significant bits on the sensors are packed into button data bytes but
the way SuperCollider updates the data it's not obvious that when what part
of the data is arriving when. There's also a small Wiimote status UI I want
to build, that shows some basic info like connectivity, battery, MAC address,
and LED light status.

Advanced functionality may remain elusive, such as sending a sample to the
speaker. The way that communication works over the HID interface, or as near
as I can currently figure, is that each byte in the packet is configured
independently, and is also cached and only sent if different. So I'm not
sure how a 24 or 32-byte packet of audio data would really work in that
situation. I worry that setting each byte in the packet before sending would
actually send 32 bytes. I'm not confident in that observation, I could probably
verify it with some of the debugging trace code they supply, or at worst
case I imagine a BlueTooth sniffer might come in handy. Have to look in to if
one of those is handy for the job.

But, it was fun to spend some time getting to a workable Wiimote interface in
SuperCollider, even if it did render my C++ program useless. Really OK,
particularly because outside of the work on the ```hidapi``` library, which
was good learning to prepare me to work on the HID code inside of
SuperCollider, everything that I learned how to do in C++ will be directly
relevant to {% include tag_link.html tag="scintillator" %}, should that
hallowed day ever come when I have the bandwidth to work on that.

Once again I'm fanticizing about taking some time off in April to just work
on personal projects. Probably odd, I know. But I seriously just passed on
playing one of my favorite video games to write code. So taking time off
to do more of that doesn't seem too much of a stretch.

