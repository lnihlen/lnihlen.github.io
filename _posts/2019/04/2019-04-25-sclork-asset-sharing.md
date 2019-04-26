---
layout: post
title: "SCLOrk Asset Sharing"
date: 2019-04-25
tags: [ personal, sclork ]
---

Although I've been lousy about attending recent {% include tag_link.html tag="sclork" %} rehearsals, namely because
Bruno isn't there and also I'll be out of the country for their next performance in May, that doesn't mean that I
haven't been thinking about them and what I want to build next for the ensemble. We also were recently informed that
we are playing in this year's [Garden of Memory](http://www.gardenofmemory.com/), so I've been thinking about what we
could build that might facilitate a longer, more interactive performance there.

It occurred to me on the motorcycle ride in to work this morning, which is a great reason to ride a motorcycle to places,
that the area of greatest engagement that I saw in my tools and software was around the ability, built almost as an
afterthought, to share code via the chat window. Having ready access to local chat, built from the ground up to meet
our needs, meant that some of the collaborative and interpretive pieces were fundamentally changed, because sharing
code became a thing as easy as dropping the code into the chat window or pulling it out using the "Append" button I
built.

This meant that during a performance if somebody liked what they were hearing from somebody else they could just ask
for it in the chat and usually would be able to start hacking on it and modifying it within a few seconds of asking.
I've been wanting to accelerate the code sharing process, but wasn't sure how to do it in an elegant way that felt
like a natural extension of what we already have.

Meanwhile, I've also been wanting to increase the expressive power of the chat. During the performance at Dolby, the
chat was exploding in the most delightful fashion. I was thinking, particularly with the (mostly) younger people that
were using the software I made, that having memes and emjoi in the chat would probably increase the richness of the chat
significantly. But, there isn't right now a great way to share these kinds of images efficiently across the chat, and
sending the same image files to everyone or checking them into the GitHub repository seemed redundant or wasteful.

Lastly, we've had a few pieces that relied on audio sample files being shared, and the distribution of these files was
awkward, to say the least. Combine all of these observations together along with a motorcycle ride and I got the idea
for an asset distribution system, using a binary built from C++ that runs a local mirror on each ensemble laptop and
queries a central server for file asset revision control and sharing.

It was one of those exciting design ideas that ends up solving at least partially a bunch of different kinds of problems
I've been thinking about, and also opens up a bunch of new possibilities in terms of features that I had only been sort
of thinking about.

So, when I got home from work I spent some time figuring out how to set up Doxygen (which will be handy for
{% include tag_link.html tag="scintillator" %} shortly), and started in on a design document for the C++ binary part
of this, called ```confab```.

Which meant I got started on this blog entry late, which means I'll need to wrap it up now. But I'm having a good time
on these various code projects these days, which is great.

