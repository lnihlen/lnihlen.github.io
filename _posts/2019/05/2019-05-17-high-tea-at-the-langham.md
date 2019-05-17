---
layout: post
title: "High Tea at the Langham"
date: 2019-05-17
tags: [ personal, supercollider ]
---

When I packed for being out of town for almost all of May I had basically three situation in mind - hiking around the
French countryside in possibly cold and rainy conditions with field recording equipment, walking around Toulouse and
London, and working in and around the Google London office. Although folks do dress a bit sharper at the Google London
office than in California, none of those three conditions successfully anticipated the need for something nice for High
Team at the Langham London, one of the oldest continuously operating hotels in London and pretty darn posh.

So Hilary and I spent some time this morning walking around London (an activity that I was at least prepared for),
looking for some nice sweater or sports coat that I could buy so I wouldn't show up at our high tea appointment at 2pm
looking like a complete scrub. After a couple of stores with no help and nothing worth the (high) price for wearing only
once, we found a place with a helpful salesperson, a nice sweater, and a day bag to boot.

We took a short break but then it was time to walk over to the Langham for high tea. I was educated by the friendly
staff that the difference between afternoon tea and high tea is that high tea is more of a full meal. We went here last
year when Hilary and I were visiting London, and it was as amazing as I remembered. The tea here is like a whole 'nother
thing than what I'm used to in America. It's so fragrant and flavorful, I find myself wondering how I could recreate the
experience back in the states. The food is exceptional too. Both Hilary and I were stuffed by the end of the
sandwiches, and we hadn't even gotten to the scones yet!

After stuffing our faces we rolled back to the hotel, and I got some time to work on the parser for
{% include tag_link.html tag="supercollider" %}. I got an email saying that it's time to start rehearsals for
{% include tag_link.html tag="sclork" %} to get ready for our performance in late June at Chapel of the Chimes, and that
would be a perfect opportunity to debut the new tech I've been developing for asset sharing, but I'm getting in deeper
with this parser work and I'm having a hard time even just imagining a good exit point without having gained some
ground, at least landing a PR or getting one in to shape enough that if I have to come back to it in a month it won't
feel like I'm starting over from scratch.

At least today I was able to refine the heuristic on getting the tree property back from the graph returned by the C++
parser. It turns out by just removing *edges* between nodes that have a higher serial number than the containing node I
haven't been able to find a tree yet that fails to be restored by that. So that at least feels like some decent
progress. The other trick I wrote up was removing all the ```drop``` nodes, which I think are specific instructions to
the compiler to drop certain symbols from the stack? Maybe? In any event they don't add a lot of semantic value to *the
parse* itself, and I now have a function I'm relatively happy with that removes them.

So I have a (somewhat) simplified tree that is showing some more obvious relationship to the source code that went in to
the parser. It doesn't currenty include whitespace, and many of the symbols contained within each node in the tree vary
wildly as a function of node type. I'm thinking that the next step is to take the input string and the groomed parse
tree, and build a new parse tree from the ground up with normalized nodes and whitespace included. On the other hand,
I think I could also just add additional consistent properties, as well as new whitespace nodes, to the existing
parse tree. Both constructions will require a third pass through the tree, with the first pass converting the raw parse
tree into SCLang data structures and restoring the tree shape, and the second pass removing the ```drop``` nodes.

It has been useful so far to preserve the tree property that all descendant nodes must have a *lower* index, but I'm
not sure how that's going to work once I start adding in the new whitespace nodes. And right now the tree is constructed
bottom up, so that the root node right now has the *highest* index. And the parse nodes are currently stored in an
array, with many ```nil``` entries even coming from the native parser, and quite a few more added by the tree
simplification process. It might be the case that in the construction of the new tree I could just skip the second pass
of dropping nodes, because the algorithm to construct the new tree from the old one could just ignore them.

Anyway, that's kind of where I was when I ran out time, after looking a bit at how I might be able to take a
```Routine``` and make a pre-order tree traversal iterator out of it. Hilary woke up from her nap and it was time to
walk over to a nearby West End theater to see the stage production of Lion King. It didn't fail to entertain, with
wonderful dancing, set design, puppetry, and costumes. So another wonderful, full day in London.

