---
layout: post
title: "Return of Hilary"
date: 2019-04-15
tags: [ personal, scintillator ]
---

Worked from home in the morning so I could pick Hilary up from the airport. I'm very glad to have her home again, and
the animals are too. We all spent a few satisfying hours after dinner cuddling on the couch, starting to try and catch
up on RuPaul's Drag Race, having missed two episodes while she was away.

I also had some time to make some progress on {% include tag_link.html tag="scintillator" %}, going back to focus on the
YAML ScinthDesc file generation from the SuperCollider code side. I was able to get some simple YAML generation going,
with lots of caveats. Interestingly, the following SuperCollider code:

```
~a = ScinthDef.new(\foo, {
    VSinOsc.fg.neg
});
```

Produces the following YAML:

```
    - name: foo
      vgens:
        - class_name: VSinOsc
          rate: fragment
          inputs:
            - type: constant
              value: 1.0
            - type: constant
              value: 0.0
        - class_name: VMulAdd
          rate: fragment
          inputs:
            - type: vgen
              vgen_index: 0
              output_index: 0
            - type: constant
              value: 0.5
            - type: constant
              value: 0.5
        - class_name: UnaryOpVGen
          rate: fragment
          inputs:
            - type: vgen
              vgen_index: 1
              output_index: 0
```

which is some of the way there, but a ways to go. Actually the input code is buggy because there's no ```VOut``` output
```VGen```, so no video output would be expected. ```SynthDef``` for audio is smart enough to optimize this graph to
nothing, so if my synth generation code was as mature as that I would expect an empty graph on output. Putting that
aside for the moment, however, I'm a bit curious to go back and research how the audio code synthesizes the
```UnaryOpUGen``` with the operator type, in this case ```.neg```. Because right now I couldn't reconstruct the graph
from this, because it doesn't tell me what specific operator is being applied, only that it's unary. So that's problem
one. The second issue I have is with the inputs to the ```VMulAdd``` - actually what is it doing here at all? Seems
a bit weird to have it, and I'm curious where the inputs are coming for that.

So, obviously some debugging to do here.

After probably working on that later than I should, I went to work on this blog entry, only to discover that somehow
yesterday's blog entry, ironically named "Gentleman of Leisure," has vanished without a trace with all content except
for the header. I honestly don't even remember which computer I wrote that on (first-world problems, yeah I know), but
I think it was the workstation, and I probably lost it when I was working on font configuration, which involved multiple
vim reboots. But golly! So I've gone and hurridly added a bit of content there, just trying to detail what it was I
remember from the entry.

And now it's way too late for a work night, so going to pack it in.

