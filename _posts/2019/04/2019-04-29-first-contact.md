---
layout: post
title: "First Contact"
date: 2019-04-29
tags: [ personal, sclork ]
---

I'm flying to Toulouse this coming Sunday, staying a night there in a local hotel, then meeting a bus to shuttle me out to
the countryside, somewhere near Aulus, right on the border between Spain and France in the Pyrenees Mountains. There I will
take a class on field recording from Chris Watson, as part of the CAMP art collective. I've been told to expect unpredictable
weather, and also asked to bring such field recording gear that I have. Apparently there will be hiking to remote regions,
sometimes stopping and waiting for some considerable time, as well as some night work.

And that's all I really know. As I start to get excited for the trip I'm running through the itinerary, and the phrase
"no plan survives first contact with the enemy" is ringing true. We'll just have to see what each day brings. Should be a
great adventure.

Busy day at work, followed by some prepatory shopping at REI in the evening, so no real time to get heads down on the
Confab system for {% include tag_link.html tag="sclork" %}. I did have some time over lunch to read through the documentation
on the QUIC network protocol, which looks like its evolving into the official IETF standard for HTTPv3. There's a ton of
reference implementations, including the one inside of Chromium itself. I was thinking that might be a much cooler way
to send files around quickly on the network. But looking at the libraries, many with no or very scant documentation, all
of them in experimental state at best, and my spidey senses really started tingling that this is a serious case of
premature optimization. The documentation for Pisatche, the REST API library I'd settled on for the file exchange part
of Confab, although incomplete, seems super helpful, with a well-thought-out, intuitive API, compared to what I was
looking at today.

So yeah, another interesting design concept but ultimately discarded because of practical concerns. Maybe I'll think about
it for v2.0. But for now, conventional HTTPv1.1 is proven, reliable tech that's been powering many a Internet solution
for many a year. Should be plenty fine for Confab 1.0.

Bit sad to be back to weeknight productivity standards but them's the breaks.
