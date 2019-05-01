---
layout: post
title: "Flatbuffers"
date: 2019-04-30
tags: [ personal, sclork ]
---

I've been hemming and hawing with the design of the asset sharing system Confab for
{% include tag_link.html tag="sclork" %}. The big thing as how slick and cool LevelDB is about not making additional
copies of memory retrieved from the database or destined for writes. A lot of early optimization of any program,
naturally, is doing careful design work to remove needless memory copies from the system. Otherwise, why bother with
C++ at all? I was feeling even more design strain from the desire to have a few different ways of serializing data into
the database. For small assets, say smaller than the LevelDB page size of 4K, it makes sense to serialize the data right
inside the metadata record itself. In that case, sometimes it's string UTF-8 data and we want to respect the null
terminator, and sometimes it's raw binary data (like for the Twitter Emoji collection), so a length should accompany
the string. I was thinking of using that slick Base64 encoder for that, and serializing it to YAML. Then there's the
case where the data are potentially much larger, like for audio samples, and storing those data under a separate key
makes a lot more sense.

So, thinking about three different encoding scenarios, or two with different expectations about data format, and running
that through YAML, without extra copies of the data, was making me sad. Plus I was starting to realize that it was
becoming increasingly awkward trying to connect the YAML format I want to use to talk about assets to SuperCollider to
how they should be stored in the database. For instance, despite it making sense to me to serialize a small image to
Base64 similar to a Data URL on the web, and then send that over the wire between instances of Confab, that Data URL
format for an image is useless in SuperCollider, which very much wants to source its images from files. Assuming
that SuperCollider is providing the image file originally, it seems less than optimal to reformat that image into
a string for serialization into a database that is perfectly fine accepting the original binary data, particularly when
the binary file format is the only option into our out of the client language.

So the first decision was to break the two formats up. Let SuperCollider talk to us in YAML over OSC, putting whatever
fields it needs in there to do its work, and we can serialize to the database in a different, more memory-efficient
format. It was at that point that I remembered the brilliant work a colleague of mine at work, Wouter, had done on
[Flatbuffers](https://github.com/google/flatbuffers), which is essentially a low-to-no copy binary wire format for
arbitrary C++ (or many other languages) data containers. So, my working time this evening was focused on bringing in
flatbuffers and refactoring the original test code I had written to serialize a basic sanity-test data structure to
and from the database. After some struggling with getting CMake to automatically convert my input schema files into
the generated headers, which got a lot easier when I discovered the built-in function flatbuffers provides for exactly
this purpose ```build_flatbuffers()```, I was off to the races.

What's exciting about flatbuffers too in this context is that the wire format for exchange of data over HTTP via
Pistache just got a lot simpler too, because I can build my own data structures for the responses, putting what I need
in to them, without having to worry about parsing a bunch of YAML or anything like that.

It wasn't all roses, I *did* have a headache trying to get the Validation stuff working, and am planning on revisiting
that at some point soon. Both for stuff coming off the wire or out of the file database, I want the code to be extra
paranoid and make sure that the data its getting seem to be valid. We will be re-hashing binaries received, for example,
to make sure that they match the supplied key, and calling out warnings and error messages when they do not. The power
and network connectivity states of the laptops during a performance are unpredictable at best, and I frankly think it's
bad software design to demand of the performers that they always have a reliable upstream Internet connection, or that
they properly terminate all background processes at the end of a performance. Good software always lands on its feet,
and fixes itself if it can, and that's what I want for this stuff too.

Then there was a bit of a shuffle because the font rendering on gVim on this Gentoo Linux box was still driving me nuts.
The fonts looked pretty rough, and the screen was full of pixel artifacts after edits where it seemed that the
underlying display logic hadn't quite effectively erased whatever old character was there, leaving behind little bits
of old characters.

After a bit of Googling around I took a risk and enabled the ```gtk3``` USE flag on the gvim build. I'm still using
Plasma on this machine so I didn't know quite what to expect but I do know I run some modern gtk programs, so it's
not like I was going to be pulling in a bunch of dependencies, and I do know a *lot* has changed in the world between
GTK and GTK3. After a quick rebuild of gVim I was delighted to see the font rendering with the same level of quality
as all of the other programs on the machine. So yay!

Long days at work for pretty much the rest of the week, but then it's pack and get on a plane for my big adventure!
Can hardly wait.

