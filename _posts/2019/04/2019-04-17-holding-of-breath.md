---
layout: post
title: "Holding of Breath"
date: 2019-04-17
tags: [ personal, supercollider, scintillator ]
---

One of the more maddening parts of the Google promotion process is the eternity-feeling wait between when promo results
are decided and when they can be revealed to the candidates. We're in that hinterland right now, and since I myself am
up for promo this cycle when my reports ask me if there's anything I can reveal about their results, while I practice
my poker face with them I can at least have empathy.

We pour so much of ourselves into this process, and have so much on the line, the wait represents an additional burden
on a process that already encumbers one with such a great deal. Tonight is one of those nights where the wait feels
particularly long. I must remember to breathe.

I've started a short list of features and projects that I'd love to work on with
{% include tag_link.html tag="supercollider" %}, and am eager to begin on once the formatting discussion is put to rest.
Diverting energy away from that discussion right now feels like it would be a big error, given the importance of that
discussion for the continued well-being of both the code base and the overall development community. We're now in the
homework phase of that project, where I spent some time this evening working on a new style guideline for C++, mostly
based around the structure of the [WebKit Code Style Guidelines](https://webkit.org/code-style-guidelines/), with some
notable exceptions.

At first I thought I would document only the exceptions but the more I look at it the more I think the document will be
more useful if I include both the original style as well as the exceptions, so that readers aren't forced to flip
between two documents and keep a diff in their head just to get the piece of information that they want.

I had also had the goal of writing some unit tests in {% include tag_link.html tag="scintillator" %}, and while I was
able to make some small progress in that regard, as well as discovering some old work in this area that was largely
usable with some restructuring, I still have some parts of the ```ScinthDef``` code left to test. I did come to some
clarity around separation of ```VGen``` unit tests from ```ScinthDef```, moving the signal chain build process to the
```VGen``` tests, and then adding the parts that ```ScinthDef``` relies on, basically putting the objects in the
```children``` array and making sure that each object has a reference back to the containing ```ScinthDef``` and has
the correct index stored for itself in the array, so that the input indices will be correct in the description file.

Always more to do there, and never enough time to work on it, but that does seem to be a problem I like to have.

