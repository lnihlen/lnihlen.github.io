---
layout: post
title: "More Tap Tempo Work"
date: 2018-08-20
tags: [ supercollider, oort_cloud, i_made_a_thing ]
---

Brought in the
[foot controller code](https://github.com/lnihlen/sc/blob/061e81764796c8527ba65445cd464de1ec87be16/tap_stream_player.scd)
I had written for the first iteration of the tap tempo sequencer and tested it
out on the live drums. Not super great. There's no visual indicator of matched
tempo, and the bass line on the Minitaur makes it pretty rough to determine
what the {% include tag_link.html tag="supercollider" %} code thinks the tempo
might be.

The bass tones are difficult to hear on the in-room monitors, so probably need
to switch to the in-ear monitors, which means hooking up the headphone amp. And
probably getting that Raspberry Pi going for the visual tempo indicator,
although I might be interested in trying to find a less obtrusive visual display
to drop on my drumset than a touchscreen monitor.

Of course, there's always the dream of a
[fanless rackmount](https://www.logicsupply.com/mk020-50/) computer, racked up
in a
[super shallow rack](https://www.amazon.com/gp/product/B00ICT5H86/ref=od_aui_detailpages00?ie=UTF8&psc=1), but the shallowest rackmount KVM I can find will only
fit in a 19 inch depth rack.

I still need to figure out how to control my MOTU 16A via OSC to set the
volumes on the monitor and mains outputs. But I think the most important thing
to do at this time is to work on the visual display. Without that I don't
even know if I can use this algorithm as-is or if I need to move on to the
third revision I've been thinking of, with the explicit switch between foot
triggering control and automatic tempo scheduling.

Time to go rack up some parts and figure out that Raspberry Pi. Found
[this](https://www.modmypi.com/blog/raspberry-pi-7-touch-screen-assembly-guide)
setup guide which seems the most clear for getting the touchscreen going.

