---
layout: post
title: "Shut-In During Shutdown"
date: 2019-01-11
tags: [ personal, sclork ]
---

The best anecdote that summarizes the day is that around 5 PM a hotel manager,
accompanied by a security detail, knocked on my hotel room door. Apparently I
had left the "do not disturb" light on for 24 hours and it's hotel policy that
they check on guests that do that, just to ensure there's no trouble. They
went away with no trouble once I appeared at the door looking sober and
uninjured, with no sign of the hotel room behind me in disrepair.

I swear I had left the room at least to get dinner yesterday evening, so I don't
think that I actually spent 24 hours in this room without leaving, but it might
as well have been. It's now several hours after that incident, and short of
riding the elevator downstairs to pick up some takeout for lunch and dinner I
have been mostly here.

I took some meetings in the morning over videoconference. Everyone else was
traveling back home to California today, and should I attend CES again next
year I would hope that I would have the presence of mind to read back here, or
remember, that the best way to do CES I think is to travel on *Monday* and
*Friday* of.

I also had some vague plans to head back over to the convention this afternoon
but once my work responsibilities were largely over, modulo the constant
monitoring of my email inbox which is pretty much awake to asleep.

In the evening I was able to grind out a great deal more code for
{% include tag_link.html tag="sclork" %}, pretty much finishing the first
implementation and unit tests of SCLOrkWire inside of the
[SCLOrkNet](https://github.com/lnihlen/SCLOrkNet) Quark. I'll need to update the
documentation, and then will have to transition over to a refactor of the
[SCLOrkChat](https://github.com/lnihlen/SCLOrkChat) Quark to use the new
reliable protocol code.

That will prove out the implementation of the Wire code in a real-world
deployment. Then it will be time to return my focus to the
[SCLOrkClock](https://github.com/lnihlen/SCLOrkClock) Quark, using the Wire
stuff to handle the control protocol, as well as a re-implementation of the
clock synchronization code to use Kalman filters, as the discussion on the
SuperCollider user's mailing list turned up
[another implementation](https://github.com/jamshark70/ddwOSCSyncClocks) of a
network clock by the inimitable *Jamshark70* that does so, following the recent
Abelton Live sync work, and I think that's just dandy.

I've been enjoying watching some PBS while stuck in the hotel room. They just
had a neat documentary and interview with the director
[Sydney Lumet](https://en.wikipedia.org/wiki/Sidney_Lumet). Think when I get
home tomorrow I'll be suggesting that we work our way through his films next.

Tomorrow I get up early-ish and head to the airport to fly back home. Hopefully
both weather and the vagaries of government shutdown will be kind to those
plans.

I worked at a startup where the boss wanted us to continue working indefinitely
without pay until funding issues were resolved. I think the folks who are
continuing to work deserve our respect, but so do as well the folks who have
decided not to work. I cannot possibly imagine how difficult their situation
must currently be, regardless of their choice.

The parting words of the Sydney Lumet documentary was a quote from Mr. Lumet,
something to the effect that he felt fortunate enough to have paying work in
a field that he felt mattered and that he enjoyed. Feeling grateful for that
myself, right now.

