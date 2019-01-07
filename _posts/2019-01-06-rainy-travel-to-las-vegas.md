---
layout: post
title: "Rainy Travel to Las Vegas"
date: 2019-01-06
tags: [ personal, sclork ]
---

This is my second trip to CES, my first being last year as the newly-minted
manager of the client teams for Google Play Movies & TV. It's a huge convention,
taking over 3 different convention centers here in Las Vegas, and selling out
nearly every hotel on the strip.

It being my second time, I'd like to think I learned a few lessons from the
first trip. One lesson I didn't learn very well apparently was to book travel
as early as possible, because plane tickets also fill up fast. So when I booked
travel I had few options, particularly for direct flights, with everything gone
on Monday and Friday, which are the preferred travel days, and only flights
from SFO (much further from my home) available on Sunday (going out) and
Saturday (returning).

So I woke up this morning to a second day of heavy rain and started preparing.
Hilary was generous to drive me over the hill and up to work, so I could grab
my business cards, which I had printed short notice for last CES and didn't
arrive until weeks after I returned. Another lesson learned there, so awkward
to be the only person in the room who can't play during the ritual business
card exchange.

Then it was up to SFO, to wait while my flight was among the lucky ones to only
be delayed *four hours* instead of being canceled. You know you're in for a good
time when the gate agent is reassuring waiting travelers that he's
*almost certain* they'll be able to find a replacement pilot for the flight
you're heading out on. Fortunately, we did eventually get underway, and the
resulting flight when it did happen was brief and uneventful. Another lesson
learned from the first CES, where I was convinced that driving to Las Vegas
would be much less a pain (it definitely isn't), and that having access to
my car would be convenient (it definitely wasn't).

As a result I didn't hit the hotel until after midnight but all that hassle
aside I'm glad to be here. I had packed in my backpack a bunch of options to
kill time at the airport and on the flight, of course. I spent my time at the
airport plugged in to one of the plentiful power outlets available at SFO,
gleefully hacking away on the sound design project code, refining the Neuron
sound further until I was, without some kind of studio-quality monitoring
setup, pretty happy with the results compared to what I hear in my head.

I just started reading
[Designing Sound](https://mitpress.mit.edu/books/designing-sound) by Andy
Farnell, a classic in the field, and one of the first things the author
discusses is the importance of *patience* when working on sound design. I found
this comment to be helpful and sort of validating, like reminding me that I
am working on developing a new skill, it's a difficult one, and that it's going
to take time to develop an intuition surrounding how to make audio come out of
a bunch of SuperCollider code.

I was also able to make some limited progress on
{% include tag_link.html tag="sclork" %} work. I started in on a design document
for the network controlled clock stuff. Maybe third time's the charm? We'll see.
That lead me to finally put pen to paper on a rough design sketch for a
"reliable" communication class that builds a connection-oriented protocol with
packet drop detection and full duplex bidirectional communication out of
UDP-based OSC communication. Bruno is going to be firing up the
code I wrote for the first class rehearsal of SCLOrk tomorrow, so I'm hoping
that it isn't a total train wreck and I can start in on the forward progress.
The alternative is that things don't go so great, then I'll prioritize bug
fixes as he reports them. But after any immediate fires are out, and I'm not sure
how many spare cycles I'll have this week what with a few days mid-week of
back-to-back partner meetings, I'd like to be able to re-implement the
client-server communication in the SCLOrkChat quark to rely on the reliable
connection-oriented stuff I just designed, a class I'm tentatively christening
SCLOrkWire.

Tomorrow I think is when the rest of my esteemed colleagues (CES veterans all)
will be traveling, so it's likely I won't be leaving the Wynn hotel, either
attending meetings over video conference via my work laptop, or perhaps in the
evening if I have time bent over my personal laptop and hacking away. So in
other words, a pretty blissful day with room service. Maybe this CES trip isn't
*all bad..*

