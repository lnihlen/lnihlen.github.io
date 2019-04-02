---
layout: post
title: "Dentist and VGens"
date: 2019-04-01
tags: [ personal, supercollider, scintillator ]
---

So it's already apparent that a nontrivial fraction of this stay-cation is going
to be occupied in catching up with the pile of errands that have been steadily
piling up while I was otherwise almost entirely occupied with either work or
work recovery.

This isn't necessarily a bad thing - having a bunch of these kinds of tasks
backed up can really feel like a drag, particularly when they are all considered
as a whole, where they emotionally merge into one giant MegaChore.

So to the dentist for a cleaning, picking up packages after, then some work
with Hilary to finalize our tax situation for last year.

I *did* have some time to tinker with
{% include tag_link.html tag="scintillator" %}, including finishing up some
of the last little bits of the pixel light up part of the Vulkan Tutorial, as
well as having a read through both code and documentation around how
{% include tag_link.html tag="supercollider" %} converts a ```SynthDef``` into
a graph of function objects, specifically ```UGens```, which get serialized to
a file and then passed over to the server.

The key seems to be the superclass of ```UGen```, which is
```AbstractFunction```, which provides a bunch of methods to tell the object
what operations are being applied to it. An example, cribbed from the
[documentation for UnaryOpUgen](http://doc.sccode.org/Classes/UnaryOpUGen.html)
might be instructive:

```
(SinOsc.ar(200).abs).dump;
```

Which, when executed in the interpreter, produces the following:

```
Instance of UnaryOpUGen {    (0x558144b3b9c8, gc=D0, fmt=00, flg=00, set=04)
  instance variables [9]
    synthDef : nil
    inputs : instance of Array (0x558145adfac8, size=1, set=2)
    rate : Symbol 'audio'
    synthIndex : Integer -1
    specialIndex : Integer 5
    antecedents : nil
    descendants : nil
    widthFirstAntecedents : nil
    operator : Symbol 'abs'
}
```

This is the end of a chain of 2 ```UGen``` objects, the other one being what
resulted in calling a *class* method ```SinOsc.ar```, which returns a new
```SinOsc UGen``` object. The ```.abs``` is chained on to that object, and
the calls is handled by the ```AbstractFunction``` superclass, which defines
```.abs``` (along with a *long* list of other unary operators) as:

```
AbstractFunction {
...

    // respond to math operators
    neg { ^this.composeUnaryOp('neg') }
    reciprocal { ^this.composeUnaryOp('reciprocal') }
    bitNot { ^this.composeUnaryOp('bitNot') }
    abs { ^this.composeUnaryOp('abs') }
    asFloat { ^this.composeUnaryOp('asFloat') }
...

```

Now overriding this function is key, as it allows ```UGen``` to provide a
unary UGen object here with the ```abs``` operator and attach it in the
signal chain to the ```SinOsc```. And indeed the definition in ```UGen``` kicks
this off:

```
UGen : AbstractFunction {
...
    composeUnaryOp { arg aSelector;
        ^UnaryOpUGen.new(aSelector, this)
    }
...
}
```

Note that both the selector (in this case ```abs```, as well as the reference
to the ```SinOsc``` on which ```.abs``` was calld, are provided to the
```UnaryOpUGen``` constructor, which routes it back to the function that
seems to make most of the more straightforward objects in ```UGen.multiNew```:

```
UnaryOpUGen : BasicOpUGen {
...
    *new { arg selector, a;
        ^this.multiNew('audio', selector, a)
    }
...
}
```

Ending up in ```UGen.multiNewList```, which is a bit confusing as it is written
to handle the case of multichannel expansion, but essentially it's job is to
call ```args.asUGenInput(this)``` on the input array of arguments, which
we will discuss later. But for single-channel elements ```(size == 0)``` the
call gets routed to ```new1```:

```
UGen : AbstractFunction {
    classvar <>buildSynthDef; // the synth currently under construction
...

    *new1 { arg rate ... args;
        if (rate.isKindOf(Symbol).not) { Error("rate must be Symbol.").throw };
        ^super.new.rate_(rate).addToSynth.init( *args )
    }
...
    *multiNew { arg ... args;
        ^this.multiNewList(args);
    }

    *multiNewList { arg args;
        var size = 0, newArgs, results;
        args = args.asUGenInput(this);
        args.do({ arg item;
            (item.class == Array).if({ size = max(size, item.size) });
        });
        if (size == 0) { ^this.new1( *args ) };
        newArgs = Array.newClear(args.size);
        results = Array.newClear(size);
        size.do({ arg i;
            args.do({ arg item, j;
                newArgs.put(j, if (item.class == Array, { item.wrapAt(i) },{ item }));
            });
            results.put(i, this.multiNewList(newArgs));
        });
        ^results
    }

    init { arg ... theInputs;
        // store the inputs as an array
        inputs = theInputs;
    }
...
    addToSynth {
        synthDef = buildSynthDef;
        if (synthDef.notNil, { synthDef.addUGen(this) });
    }
...
}
```

So for those following along at home that call to ```.abs```:

    * got handled by ```AbstractFunction```, which called ```compuseUnaryOp```,
    * which got picked up in ```UGen```, creating a new ```UnaryOpUGen```,
    * and the ```UnarOpUGen.new``` called ```multiNew``` up in parent ```UGen```,
    * which punted it to ```multiNewList``` right below, which does some
      complicated magic around multichannel expansion but for the simple case
      just returns the results of ```this.new1(*args)```,
    * which handles the rate (```.ar``` and such, boiling down to ```\control```
      or ```\audio```), and chains both a call to ```addToSynth``` and ```init```.

Phew. Lots of indirection there but the flexibility granted is pretty incredible,
allowing for grouping of ```UGens``` by their input semantics, and making it
pretty easy for me to build my own signal graph generation system with the
```VGen``` object (again not in love with the name but golly). To finish the
story ```addToSynth``` calls a callback to a ```SynthDef``` object that is set
via a class variable ```buildSynthDef``` (ick, but it's hard to imagine a more
elegant away around this when things are being punted up to ```AbstractFunction```
during construction, which has no understanding of ```UGen``` or ```SynthDef```
objects). And the init finally sets the inputs to the ```SinOsc``` that was in
the call chain at the very beginning.

Perhaps unsurprisingly, calling:

```
(SinOsc.ar(200).abs).input[0].dump
```

Reveals the SinOsc that was originally provided:

```
Instance of SinOsc {    (0x558145b4e098, gc=D0, fmt=00, flg=00, set=03)
  instance variables [8]
    synthDef : nil
    inputs : instance of Array (0x558145b05258, size=2, set=2)
    rate : Symbol 'audio'
    synthIndex : Integer -1
    specialIndex : Integer 0
    antecedents : nil
    descendants : nil
    widthFirstAntecedents : nil
}
```

With its ```inputs``` array as two numbers ```[200, 0]```, the latter which I
suppose is the default value for the ```phase``` parameter. The numbers there
come from the fact that the ```asUGenInput``` method called during
```*multiNewList``` is defined on ```Object``` as:

```
Object {
...
    asUGenInput { ^this }
...
}
```

So those numbers return themselves, meaning that they don't propagate the
signal chain forward as the same method in ```AbstractFunction``` does:

```
AbstractFunction {
...

    asUGenInput { arg for; ^this.value(for) }
...
}
```

Which is what invoked the ```.abs``` call on the ```SinOsc``` object during
its construction. I think.

So, some design thoughts and it's prompted a few ideas but not a lot of code
generated today. On the ```ScinSynth``` side I've been looking in to both
Vertex Arrays and Uniform Descriptors to better understand how information gets
transferred to the GPU in the Vulkan world. I'm trying to determine how the
compute graph produced by the ```VGen``` code would map to Vulkan concepts
most elegantly.

In the meantime I'm holding out some vague hope that ```VGens``` could be
provided entirely by text, requiring no ahead-of-time compilation, because they
consist of some metadata, including input and output parameters and kind
(vertex, fragment, compute, etc), as well as a mess of shader code, all of which
can be compiled at runtime. What that could mean is that it could be entirely
possible to specify VGens in SuperCollider code, or perhaps in some neutral
language-agnostic textual format (honestly thinking YAML here), meaning that
VGens could be defined or tweaked without recompilation of the synth. This is
an edge over normal SuperCollider audio synthesis and I find the idea pretty
exciting.

If you've read this far hopefully you've learned something. I can see I'm already
developing the chronic insomnia that tends to plague me during breaks longer
than 1 or 2 days, so in the interest of not turning into a complete nightsider
I'll sign off.

