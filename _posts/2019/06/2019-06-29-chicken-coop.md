---
layout: post
title: "Chicken Coop"
date: 2019-06-29
tags: [ personal, chickens, supercollider ]
---

The {% include tag_link.html tag="chickens" %} had really been outgrowing their brooder, so after sleeping in a bit and
a leisurely breakfast it was time to start in on unloading and constructing the chicken coop. The plan I had been
thinking of was very loose, and had a bunch of "maybes" in it, depending on how things would go in earlier phases.
For example, I was hopeful that I might be able to back my truck up directly into the area where the coop was to be
built, rather than the driveway below it connected to that area by a series of awkward handmade stairs. That went OK, so
the next maybe was hoping that I would be able to unload the coop and run in pieces directly from the back of the truck,
that there wouldn't be any piece in there too monolithic and big that I wouldn't be able to unload it.

That mostly worked, with the possible exception of the front of the coop, which has the nest box integrated in to it for
easy egg harvest, which will be great in the roughly 5 months to go when they start producing eggs, but for today it
mostly complicated our ability to assemble the coop because it was heavier than Hilary and I could comfortably carry
together. Some dragging, shoving, and sliding it around probably marred the paint on the front a bit more than was
strictly necessary but in the end we were able to swing it.

The last area of doubt was mostly around if we were going to be able to actually assemble a usable coop and run, meaning
that the instructions were useful enough, all of the right pieces were here (or at least all that couldn't be readily
replaced), we had all the tools we would need, etc. Another pleasant surprise was to see the electrical wiring kit
included, which I had ordered to be delivered separately to our private mailbox, instead of directly to our home like
the coop, but it had never arrived. They had packed it directly in to a hollow space along with the rest of the pieces
of the coop, so it did arrive after all, and no sooner than was strictly needed.

The coop came together pretty easily, and I was impressed by how closely the pieces fit together consistently on all
sides, yet not really requiring a whole ton of effort to get them in to the right place. A good balance between a tight
fit but not requiring a whole lot of prying and shoving in order to get things to line up. Fit and finish looked solid,
and a careful scan through the interior revealed only a single nail mislaid that looked like it could maybe injure an
inquisitive chicken, which I promptly removed.

The run didn't come together as easily, as this was a series of large steel frames with chicken wire tack welded on,
that needed to be bolted together using provided hardware. The roof was challenging, because of the need to hold up
the heavy roof sections overhead while at the same time aligning the corners for the fastening. Hilary and I toughed it
out, however, and in the later afternoon I was glad that we were able to move the birds in to their new home.

As they had been living in a large plastic storage container with a roof of plastic hardware netting I think their minds
were a bit blown when we released them in to the chicken run for the first time. That's a pretty small space, which they
were outgrowing, into a very large space, and the first time (likely) that they have been outdoors. It was interesting
to watch them, they kind of wandered around a bit before hopping back in to the brooder, which was still sitting in the
run with the lid off.

So, I started loading them through the chicken door into the coop, which I think they found much more familiar, although
it too is significantly larger than the brooder they had been in. At least it has a roof overhead, however! That's
pretty much where they remained, at least as far as we could tell, until we came back a bit before dark to close them
in for the night. I am curious how long it will take for them to feel tempted to explore the run again.

After a bunch of time away from my phone while I was working outdoors I was delighted to notice that Tom Mudd, the
musician who had created that Duffing-equation based album I mentioned yesterday, had responded with a nice email to my
purchase of [his album](https://tommudd.bandcamp.com/releases) on Bandcamp! Turns out he had read my blog post from
yesterday, and had some helpful advice about implementation details, including a reference to an
[excellent textbook](https://ccrma.stanford.edu/~bilbao/nssold/booktoplast) from Sefan Bilbao about numerical methods
for audio synthesis.

I'm always a bit surprised when someone mentions that they read something on my blog, and doubly so if they said they
found it interesting! So that was really cool. It made me even more excited about implementing my own version of the
Duffing equation in SuperCollider, and I started digging in to that a bit more by noodling with some code as well as
reading up a bit about Runge–Kutta-Nyström methods, which are ideal for iterative solutions of second-order differential
equations like the Duffing equation, although they are generally applied in situations where the first derivative terms
are zero.

There's [a paper](https://ntrs.nasa.gov/search.jsp?R=19740026877) from NASA in the 1970s that derives a general-purpose
RKN integrator. Always cool to run in to the [blue meatball](https://en.wikipedia.org/wiki/NASA_insignia) in my travels.
Also figures that, given orbital mechanics equations are mostly second-order differential equations, that they would be
interested in efficient integration of these formulae from back in the day. It's getting late tonight but I might
consider that being the place where I start next time I look at this, which will hopefully be tomorrow.

And, of course, I realize that I haven't yet booted the SuperCollider audio server tonight! So I'll wrap up here and
quickly try to make some sounds before bed.

