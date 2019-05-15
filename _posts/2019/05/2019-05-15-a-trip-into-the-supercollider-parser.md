---
layout: post
title: "A Trip Into the SuperCollider Parser"
date: 2019-05-15
tags: [ supercollider ]
---

While on vacation here in France I've been spending some time looking in to the SuperCollider parser so I thought I'd
come up for air and talk a little bit about what I've learned so far. This post will be focused entirely on that.

For context, there have been a few occasions recently where I thought having an ability to convert a SuperCollider
program from a string into a parse tree, and then back again to a string after some manipulation, would be quite
convenient. The first was in building a semi-automated software development tool for use in a structured performance
by the laptop orchestra I perform in, {% include tag_link.html tag="sclork" %}. The most recent need for this has arisen
from the desire to have some more sophisticated automated linter/formatter tools available for the SuperCollider code
base itself, which includes some nontrivial SCLang code in the form of the class library.

Currently, although it is possible to compile an arbitrary string as SCLang code from within the language itself, it is
not possible to only *parse* it, and therefore extract the parse tree that the compiler makes during the course of
compilation. My plan has been to write some C++ code that could marshal the parse tree back to SCLang, possibly
post-process the tree a bit more on the SCLang side, and then expose the tree for manipulation by other programs.

To complete "the round trip," that is from ```code -> parse tree -> modified parse tree -> modified code```, the
parse tree must have an *unambiguous single owner* for every character in the source input. The "owners" of individual
tokens within the source can have children and parents, to help establish the context of the token in relation to other
parts of the source, but the invariant needs to be that by modifying the "source" attribute of an individual parse node
a sensical modified source code can be constructed from that parse tree, with modifications intact.

I have [a PR](https://github.com/supercollider/supercollider/pull/4402) up on the site which can show some of the
progress on this work. Given that we've decided to move forward on the C++ code formatting project this PR isn't at the
very top of my priorities list anymore, but it does show my progress to date.

What I've learned is that the parse tree currently being produced by the parser wasn't ever built with the idea that it
would need to be mapped back to the source. It is obvious that this was very much a one-way process from input string
to parse tree to compilation.

I'll skip to the end product to try and add some clarity to the discussion, then step back and share some of the other
learnings. I made an HTML tool, [ParseVis]({{ "assets/html/blog/2019-05-15/index.html" | absolute_url }}) for exploring
the output of the parser. On the left on that page is the code input to the parser, in this particular example it is the
SCLang script that actually generates the JavaScript inputs that this very HTML page consumes (how meta, I know!).
On the right is an ordered, numbered list (with several consecutive elements missing, you may note) of all of the nodes
in the parse tree. If there's textual information attached to the node it has been included in the listing. You may
note that not all of the nodes have textual information. There is an enumerated type included in each parse node, which
I have a text description of included after each node's unique id number.

If you mouse hover over one of the nodes on the right there's some JavaScript on the page (and yes, I'm a horrible
HTML/JS developer and will probably never take the time to become a better one) that will highlight a few things,
described here. Unmodified, ```PyrParseNode``` and its diverse descendants, which are the actual tree of objects
produced by the parser, keeps track of only a line number and character *within that line* (so more accurately called a
column) for each parse node. The impression I get is that they are primarily used to report compilation errors back to
the user after parsing. It is clear that the parser itself has no interest in keeping any kind of firm relationship with
the underlying text for purposes other than user feedback.

The line and column numbers are kept in global variables and copied into the relevant ```PyrParseNode``` during
construction time. There were two other globals of interest, one tracking the actualy byte offset within the source
text, and another with some concept of length. I have added some C++ code to the parser to include these globals in each
ParseNode it constructs as well. As one hovers over the individual parse nodes on the right the JavaScript I wrote will
highlight in red both the individual character in the source string indicated by that global at construction time, and
the length. As I have observed that the text position is usually toward the end *or even just past* the end of the part
of the source code that the parse node seems to be relevant to I have made the assumption that the length refers to
characters *backwards* from the text position in the parse tree, so the length extrapolation is also highlighted in a
lighter color of red.

One thing you may observe about that is that the positions identified by the parser are only approximate, and typically
are ahead of the relevant symbol in the code by somewhere between zero and three characters. In fairness to the parser
code (which again I must emphasize was never designed to be used this way) I will remind the reader that I am exposing
a global variable here that was not intended for use for anything other than the internal operation of the compiler.

In the ParseVis tool, hovering over an individual node will highlight the children/contains list of nodes in blue, and
the parents/containedBy list of nodes in green. Another thing to explore is that, in this particular example, nodes 22,
14, 45, and 54 (along with perhaps others), all have *two parents*. This is why I have settled on this admittedly
awkward tree visualization format, which is in fact that this isn't a tree at all, it's a directed acyclic graph. At
least it is acyclic! The discovery of the multiple parents situation I made by staring confusedly at printouts of parse
tree serializations and realizing that I was seeing the same ```variableDefinition``` nodes come up again and again in
the parse tree. It's probably the most significant step forward in terms of understanding the parse tree output that
I've made to date. For the few different files that I've looked at, the only nodes that are guilty of having multiple
parents are ```variableDefinition``` nodes, so perhaps there can be some simplifying step here where I can restore the
tree shape of the DAG automatically.

I also added the node id numbers, to aid in detecting the multiple-parents situation. This is another global that I
added that sits alongside its siblings in PyrLexer.cpp, but gets incremented inside of the ```PyrParseNode```
constructor, after storage in the constructed node. It's the easiest way I could think of to provide a *reference* to
a node, therefore allowing me to make lists of referenced nodes instead of lists of nodes directly, thus creating a
data structure that is tolerant of duplication of nodes (and could even handle cycles if there were any).

Using the node id numbers has also revealed that there are some nodes that get created during the parsing process that
end up unreachable in the finished product. You may note from the ParseVis that while the indices increase monotonically
there are frequent gaps. Given that the ```PyrParseNode``` constructor is the only point where the node id counter gets
incremented, it must be that those nodes get created but are ultimately dropped, perhaps coalesced into other nodes or
elided. This may have something to do with the ```drop``` nodes that are common throughout the parse tree, but I haven't
investigated much further.

As an aside, the concept of "parent" and "children" in this parse tree is already a bit of a simplification. If you look
at the actual attributes for the individual nodes, the fields that point to possible subtrees within a given node all
have node-type specific names. So, for instance, in ```block``` type nodes there are three subtrees, one with the name
```variables```, one named ```arguments```, and the last named ```body```. This makes sense for a block, because those
are the things that are contained within a block of SuperCollider code. As a post-process step I take all three of those
lists and concatenate them into a single IdentitySet, ```contains```. I can then iterate through that list for each node
and build a new IdentitySet, ```containedBy```, which is then rendered (after translation to JavaScript data structures)
in the ParseVis tool.

So at this point to me very little is clear except that there will need to be substantial additional processing on the
output from the C++-based parser in order to be useful toward the end goal. I'm going to take a short break from this
work and shift my attention back to the other tasks I had piled up, having interrupted my work on the asset system for
{% include tag_link.html tag="sclork" %}, itself was interruption on the ongoing work on
{% include tag_link.html tag="scintillator" %}, which is starting to feel quite neglected. I'm not entirely sure if
I'm going to pursue a direction where I try to groom this parse tree into a usable form or use the parse tree, along
with the provided input source, to construct a simplified/regularized parse tree. It is at least some small comfort
that in order to complete the "round trip" I will not need to reconstruct the tree as provided by the C++ parser output
from the simplified tree, meaning that whatever simplifications or reconstructions I make can be destructive.

In summary the remaining work seems to be:

  * Figure out (in some cases like ```drop``` or ```push``` nodes) and document the meaning of the various node types,
    their members, and meaning in the parse tree.
  * Devise a consistent means to precisely identify the regions in the input string that are referred to by the node
    types. I'm currently envisioning a type-specific adjustment to offsets, which is probably the result of the parser
    being in slightly different states when creating different types of parse nodes. At least for many of the more
    obvious literals and names there is also a copy of the symbol attached to the parse node, which greatly aids in
    checking heuristics around alignment.
  * Write code to groom the provided parse DAG back into tree form. Realistically, the ```contains``` and
    ```containedBy``` structures may be doing more harm than good, and this problem may vanish when considering the
    different contexts that subtrees may be included in parse nodes in. For example, it could be the case that the only
    problem here to solve is figuring out a way to consistently consider ```variableList``` ownership by containing
    ```variableDefinition``` nodes.
  * Inject whitespace into the current parse tree, or be sure to include it when contructing a new one.
  * Devise an algorithm for identifying a single unambiguous "owner" for each token (and whitespace character) within
    the parse tree. The guarantee the parse tree needs to be able to provide is that an ordered traversal of the parse
    tree while printing or appending the substring provided by each owning node should result in a perfect
    reconstruction of the input tree.
  * Ensure that such designs allow for meaningful manipulation of the tree for tools like a linter/formatter.

It's feeling like a mighty tall order, but there's a broad variety of tools I can imagine one would make using the
parser output. Also, building a parser from the existing C++-based parser *still* feels like a much preferable option to
building a new parser from scratch, because at least by using the same parser that is used for code compilation and
execution one is confident that the parse tree provided has some real bearing to the actual execution of the code,
including not only any bugs in the parser but any further extensions or improvements that might be made in the future
to the SuperCollider programming language.

