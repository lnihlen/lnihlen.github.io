---
layout: tag_home
title: "Tag: vcsmc"
tag_home: vcsmc
---

[VCSMC](https://github.com/lnihlen/vcsmc) is my attempt to build a video player
for the Atari 2600 game console. Another name for the 2600 is the Video
Computer System, so the acronym VCSMC is an homage to the
[Xbox Media Center](https://en.wikipedia.org/wiki/Kodi_%28software%29), now
called Kodi but formerly XBMC.

A quick summary of the backstory is that for 3 years or so I worked on the
YouTube Living Room team, doing some
of the early work on getting a client on to the video game consoles. It became
time to move on and my manager then gave me a parting gift of a custom-painted
Atari 2600 console and cartridge, made up in YouTube colors and branding.

This kicked off a years-long fascination with the challenge of getting video
content of any kind to render on the machine. The
[Stella Programmers Guide](https://alienbill.com/2600/101/docs/stella.html),
originally published 2 years after I was born, is a good place to dig in to
the details about writing code for the VCS. Tl;dr is that it's hard because the
platform is unbelievably constrained - 128 bytes of RAM, no frame buffer, 4-bit
mono PCM audio, bright neon 7-bit color on NTSC, and a RISC CPU marching along
in lock step with the scanning electron beam in the CRT. They used to write
assembly for games using a piece of graph paper showing the timing of the CRT
beam as it moved across the screen tracing a path through the scan lines.
