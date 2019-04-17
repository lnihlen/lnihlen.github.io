---
layout: post
title: "Finding that Rhythm"
date: 2019-04-16
tags: [ personal, supercollider, scintillator ]
---

With Hilary back in the household we've quickly found our stride again and it feels great. There's a burst of work
coming next week to wrap up Perf but by and large it's back to our regularly scheduled programming there as well. Plus,
with vacation coming up shortly I'm starting to feel somewhat excited about my current state of affairs.

Had a longer discussion with another {% include tag_link.html tag="supercollider" %} developer earlier about the current
state of affairs around the code style formatting discussion and I think we have figured out maybe some of the reason
behind the strong pushback. I'm hoping we can get to a good place where folks on both sides of the debate feel like they
got what they wanted. It's that elusive (but priceless) "third outcome" to most arguments that I think is best, and
always worth holding out for if you can.

I had followed some of what turned out to be pretty bad advice on the System 76 tech support about using the
```nvidia-settings``` app to try and set up a dual-display 4K monitor situation on the Oryx Pro laptop and, after
a requested reboot from that program, found the laptop was crashlooping. Super great. Linux, I love you and all but
some of this trickier stuff I don't know if we're ever going to be in a super consumer-friendly world with. It pains
me to say it, but my MacBook Pro, terrible keyboard and all, works out of the box when you plug a keyboard, power, and
external monitor in to it. It fires right up and is a useful computer.

Fortunately I was able to boot off the recovery partition, which is all too happy to just wipe your install and start
over. I just had to delete the offending ```xorg.conf``` file that the settings program had generated, reboot back in
to normal installation, and everything was fine. But if I hadn't been basically rolling my own ```xorg.conf``` on
Gentoo for years I would have been completely stuck. A little disheartening to think about the dream of Linux for the
masses (outside of phones, of course).

Then I had a bit of time to work more on the Scinth generation for {% include tag_link.html tag="scintillator" %}. I
found the bug to the ```VMulAdd``` that was being added with the weird arguments, then figured out how the operator
parameter is being serialized over on the audio side for the ```UnaryOpUGen```, when all that the ```SynthDef``` file
format supports is the name of the ```UGen``` as well as a strict enumeration of inputs and outputs. Originally I had
figured it was being supplied as another input, but a read through the code reveals it's actually appended to the name
of the ```UGen```, so something like ```UnaryOpVGen_neg``` for the negation operator. Makes sense, and the name is
fair game to alter, particularly given the fact that each of the operators are mathematically distinct.

I need to write some code to contain the outer YAML, then will turn my attention to adding some basic unit and
integration tests. Been wondering a bit how to test this stuff, it's not super obvious to me. Well, not all of it
anyway. I understand that the YAML generation and ScinthDef build process should clearly be separated. For build testing
I can construct a few simple chains of ```VGen``` objects and then vet the data structure that the ScinthDef constructs,
making sure that inputs are set up correctly and everything looks sane. For YAML generation it would make more sense
to start with prefabricated built ScinthDefs, then convert them to YAML, then parse the YAML using the built-in
SuperCollider parsing, then validate that the YAML parsed correctly and that it has all the right pieces in there.

I guess it's not *that* much of a mystery after all. More like just an evening of writing some good solid unit testing.
I'm wanting to get that started so that as I add more sophistication to the build process (and lots needs to come), I
can continue to build the tests alongside it, thus continually validating the code. Also I'm imaginging some similar
testing needing to happen on the C++ side so whatever conventions I discover about testing on this side will have
their mirror over there.

But after making sure the basic functionality is well covered with testing I think I'll finally be able to close this
fork and start in on bringing the C++ code in to the main [Scintillator Quark](https://github.com/lnihlen/Scintillator)
and implementing the YAML parsing side over there as a beginning to the server-side ScinthDef build process. That's
the most exciting work on the horizon so I'm eager to get going on that.

It also looks like some of the code style questions are finally being wrapped up on the SuperCollider side, too, so
perhaps that means I'll be able to adopt a consistent C++ coding style there too. Which would be another itch I've
been meaning to scratch. So, lots of coding in front of me that seems exciting. Hoping there will be time in the coming
weeks to tackle it.

