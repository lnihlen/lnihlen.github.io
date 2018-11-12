---
layout: post
title: "SCLOrk Prep"
date: 2018-11-11
tags: [ personal, sclork ]
---

Had an {% include tag_link.html tag="oort_cloud" %} gig at the Blue Lagoon in
downtown Santa Cruz last night. About a quarter into our set the manager of the
place stopped our set and asked that we turn it down. We are a very loud band,
and I can remember playing a house party or two where we've been asked to turn
down, but this was the first time in an actual venue. It was a bit of a buzzkill
but we got it back, and then Mikey broke a string on his bass. So, bit of a
disaster gig but it was fun. We've got another one coming up with Wednesday
night.

After a few days of being distracted by {% include tag_link.html tag="vcsmc" %}
work I had to dig back in tonight to work on a few things for SCLOrk, as our
next rehearsal is tomorrow.

First order of business was to get the laptops we use for the performance
working with the NFS file share I had going on the shared server. Turns out,
they didn't have any of the necessary NFS software installed, so it was a simple
matter of `sudo apt-get install nfs-common` and I could mount the endpoint
using NFSv4. Some mucking about with permissions means anyone can read files
there but only owners of those files can write. Did a bit of mucking around with
the `/etc/fstab` file too, so that folks don't have to run `sudo` to mount the
partition, but there's some difficulty in getting the user to unmount. I Googled
around a bit but none of the suggestions I found seemed to be working. I think
folks mostly shut down the laptops when we're done, so perhaps that automatic
unmount will work.

Next I spent a minute fiddling with my
[chat program](https://github.com/lnihlen/sc/blob/master/classes/SCLOrkChat.sc)
to add autoscroll to the bottom of the TextView whenever there is a new chat
added. It wasn't immediately obvious how to do, and in fact Googling around I
found two different feature requests on the Supercollider repository, both
years stale and closed, asking for some support for this. I started thinking
about flipping the TextView around in terms of chronology, meaning that I would
add new text to the top and let the old stuff scroll off down below. But, as
a last-ditch attempt I tried setting the text selection to the last character
in the combined TextView string after each insertion, and that worked great
to scroll to the bottom automatically.

Last thing is to see if I can get command-line multitrack recording working
from the MOTU 16A in the rack to the rackmount server. I found
[ecasound](https://ecasound.seul.org/ecasound/Documentation/ecasound_manpage.html),
which seems to have some potential, including support via OSC, but also hasn't
seen any development since 2015, with several dead links in the documentation.
Still, just because something hasn't been touched in a while in the software
world doesn't necessarily mean that it shouldn't be used, it's also not the
most encouraging of signs.

In any event, I don't know if I can devise a test signal with 8 or so channels
without some fiddling, so this might have to wait and we can use a laptop
tomorrow or something to record to. I *can* record something maybe from a
stereo source, so will work on that first.

I think we're going to polish off this entire season of Great British Bake Off
in one day.

