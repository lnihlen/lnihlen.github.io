---
layout: post
title: "Pecan Pie and LibAV"
date: 2018-11-21
tags: [ personal, vegan, vcsmc ]
---

My first attempt at {% include tag_link.html tag="vegan" %} pie today, a pecan
pie per both my childhood memories and also request of Hilary. This called for
vegan butter/margarine, which I had heard about but not tried before, in both
filling and crust. It also called for making a flax egg, which is ground flax
seed in water, and is expected to have similar binding properties to a chicken
egg, and is a common substitute in a lot of vegan baking recipes I've seen for
eggs.

I had also heard of some new prepackaged vegan egg substitute that some of the
vegan baking blogs I read are really raving about, so I was trawling through
the "alt" refrigerated section of whole foods looking for that, thinking it
might be interesting to try in the filling instead of the flax egg. Every time
I go through that section I'm impressed by the number of new prepackaged vegan
processed foods I'm spotting there. This time I spotted vegan sour cream and,
right next to it, a sour cream and onion dip container.

I appreciate the explosion of vegan products and alternatives. I hope that helps
more folks consider veganism as a viable alternative. But one thing I was
thinking is that this is the second time in my life that I've made pie crust
from scratch, and the reason that I am making my own pastry crust now is that
you can't purchase pre-made pie crusts that are vegan. Yet. One of the things
I've enjoyed about going vegan is that it forces you to cook stuff from scratch.
For example there aren't a lot of vegan options in Santa Cruz, which is kind of
surprising if you think about its hippie reputation, and so if you want
something other than another order from Hong Kong Charlie's you are probably
better off making it for yourself.

This also goes for any of the vegan versions of omni comfort food like pizza or,
in this case, pie. So it's been fun learning how to build my own vegan versions
of these kinds of foods. I'm not sure, should the day come when I can buy
premade vegan pie crusts, that I'll go back to buying the prepackaged stuff.
Once you go to the trouble of learning how to make something like pie crusts or
pizza dough yourself, for me at least the idea of buying those premade seems
less fun. Besides, it always tests better if you make it from scratch, right?

![pecan pie]({{ "assets/img/blog/2018-11-21-1.png" | absolute_url }}).

The pie is cooling down now, once its at room temperature I'll bang it in the
fridge and I'll be having a slice for breakfast with a glass of Oatly, a vegan
version of an old holiday tradition for me. I'm sure it'll be different from
the omni version but hopefully not a complete disappointment.

It was also raining all day so I got some decent headway in on
{% include tag_link.html tag="vcsmc" %}. I'm working on combining three
different examples of `libav` to decode directly into my own `vcsmc::Image`
objects. I refactored those today to accept planar data, which took me down
a whole rabbit hole of representing Atari color values in both RGB and Lab
space. The `libav` documentation is pretty scant but there's a lot of different
examples running around that do part of what you want and so can be repurposed.
Of course, the first one I found uses all deprecated functions so I'm working
from a couple different things. I didn't get all the way there but hopefully
can wrap up the decoding part tomorrow.

