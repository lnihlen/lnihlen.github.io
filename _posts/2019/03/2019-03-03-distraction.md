---
layout: post
title: "Distraction"
date: 2019-03-03
tags: [ personal, scintillator ]
---

Hilary had that all-weekend training so I was on dog parenting duty, which kept me out of my office
and sitting on the couch in the living room, to keep an eye on everyone. Not that I would have
gotten much benefit out of an office today. Still very much feeling the effects of a difficult week,
and very much aware of another full week, if not a difficult one, starting tomorrow morning.

I *did* manage to start in on the mountain of paperwork due from me by Tuesday evening, including
preliminary drafts of evaluations on all of my reports, as well as, of course, additional polishing
on my own performance report.

I did have a little time to tinker with {% include tag_link.html tag="scintillator" %}, although that
was mostly spent reading documentation about the client-server communication that happens between
SuperCollider parts ```scsynth``` and ```sclang```. My hope is to build a similarly rich set of
communication tools between ```sclang``` and ```scinsynth```, or whatever the name of the C++
Scintillator binary ends up being named. I'm thinking of writing the design documentation, even for
the server, in the ```schelp``` format, because then it all sits nicely in the SC IDE, and I've found
that to be a pretty good way to build stuff for {% include tag_link.html tag="sclork" %} that way.

I learned a lot about the structure and format of the synthdesc files that ```sclang``` parses the
SuperCollider code into and then uses for describing a ```SynthDef``` to the server. It's a packed
binary format that can be serialized to a file or sent (I think) as a binary blob inside an OSC
message directly to the server.

Reading the SC synth code and the design documentation I'm again struck by how complex and interesting
the behavior is that can emerge from such a simple, elegant underlying design. James McCartney, the
original author of SuperCollider, developed it privately for his own use before releasing it to open
source a few years later. He's since moved on to other projects, saying that (although this information
is much looser than secondhand) SuperCollider no longer held his interest. Looking at this
code, the design he made, I feel as though I'm studying the footprint of a giant.

I kept a string of terrible action movies playing on the living room TV and studied documentation
all afternoon, until it was time to transition to work. Hilary came home, we had dinner, and the
weekend came to a hopefully restful but certainly unsatisfying weekend, creatively speaking.

That is what the job currently requires, I suppose.
