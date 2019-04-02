---
layout: post
title: "A Day in Monterey"
date: 2019-03-31
tags: [ personal, supercollider, scintillator ]
---

We drove down yesterday afternoon for an overnight stay in Monterey. Then up
this morning for the {% include tag_link.html tag="supercollider" %} developer's
monthly conference call. I've been skipping them for a while and given the
current situation in flux I think it's important for folks to show up to support
the developer community.

Hilary and I then popped over to the Monterey Bay Aquarium for a look through.
We used to come down here all the time, but recently have been opting to take
longer breaks and head for Disneyland instead. It was good to revisit Monterey,
the landscape is beautiful, and the aquarium is something else. The weather
having turned recently, and it possibly being Spring Break season meant that
the place was completely jammed up with people. So it was a bit overwhelming,
but still great.

Hilary loves the Sea Otters but my personal favorite is the Deep Sea experience.
A whole school of fish swimming in a constant, slow torus while other larger sea
creatures move through and around in a giant aquarium. The light is low,
allowing the rays of sunlight to show as they pass through the water. There are
some benches upstairs and chill ambient music plays softly in the background.
Because it's so dark most folks, even the hordes of screaming children that
occupy the aquarium on a beautiful Sunday like today, instinctively lower their
voices and chill out a bit. It's kind of like the chill-out room at a baby rave.

Then it was home, with enough time for me to make some pizza for dinner and
set down and grind through the remainder of the Vulkan Tutorial to get
*first pixel render* in {% include tag_link.html tag="scintillator" %}. I'm not
going to dedicate the headline to that event until the pixels are genuinely
ones from a hard-coded (at first) synth of my own design, but it still was
a pretty exciting moment:

![First Pixel Render In Scintillator]({{ "assets/img/blog/2019-03-31-1.png" | absolute_url }})

Ah yes, the famed RGB triangle of joy. It's been a long road here, and honestly
a bit of the stuff towards the end was rushed and I was just sort of jamming
it into the framework for the rest of the code that I've hastily assembled.

I need to think about next steps here. I think it's time to dig in to the
source of both supernova and the SynthDef function on the SuperCollider side.
I need a better understanding of how the Synth graph is constructed, and what
messages pass between language client and synth server in the process.

I think also getting some logging sophistication in place early will also pay
off a lot, so I think I'll be pulling in [glog](https://github.com/google/glog),
which I am pleased to see is open source and therefore usable here. Speaking of
tools I've discovered at work that are awesome, there's also
[Chrome Tracing](https://aras-p.info/blog/2017/01/23/Chrome-Tracing-as-Profiler-Frontend/),
which looks like it has at least one nice option for adding to one's own
projects. So yay, lots of cool/fun projects coming up for Scintillator.

