---
layout: post
title: "Packing Day"
post: 2019-05-04
tags: [ personal, sclork ]
---

Today was a mixture of final planning and packing for the trip and hacking on {% include tag_link.html tag="sclork" %}. On the packing
I'm using both of the family's large suitcases, but Hilary has graciously volunteered to pick up some additional luggage to support her
trip out to Toulouse when she catches up.

I'm bringing quite a lot of stuff, but in my defense I'm planning for an expedition into the French backcountry that is also a class
in field recording, so hiking boots and sport clothing are must-haves. Then there's also all the recording gear. My third week away, I'm
also working from the London office, so there's some work gear to haul as well, but not much. But it all adds up.

On the {% include tag_link.html tag="sclork" %} front I've finished another round of refactoring on the ```Database``` object inside of
Confab. I pushed almost all of the logic out of Database, making it mostly just a thin layer around LevelDB. Outside of key generation
most of the code is almost generic enough that I'm thinking of a better way to abstract it into a single read function. I'm thinking
that it might make sense to centralize the object serialization and deserialization into Flatbuffers into a separate class, and then
allow for some extensions of that. I think the decision there is to wait until I'm also sending and receiving these objects over HTTP,
to see what plays out there. It was clear that most of that logic around that should move out of Database but I'm not quite yet to the
place where it has a home elsewhere I'm happy with. 

Then I got the OSC endpoint up but didn't have time to test it. I'm thinking a good first pass through the asset addition code will
be to add the SuperCollider code to support file addition, and then write a script in SC to add all of the Twitter Emoji as image assets.
That lead me to thinking I really need a file system abstraction, and so some digging into the new C++-17 file system abstraction.

I've tried to pack as much documentation as possible on my laptop for tomorrow's overnight flight. The last few long flights have been
great for productivity. Looking forward to this one being the same.
