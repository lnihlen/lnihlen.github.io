---
layout: post
title: "SCLOrk Release"
date: 2019-01-30
tags: [ personal, sclork, vegan ]
---

I am please to report that the {% include tag_link.html tag="sclork" %}
Performance over lunch went off without a
hitch. We were performing in the lovely concert hall on Santa Clara University
campus, in the Music and Dance building. This was part of a new music festival,
and we shared the bill with two piano pieces written by emeritus faculty from
SCU, performed by the current department head. They were "extended technique"
pieces, meaning that the performer was also strumming the strings on the
beautiful grand piano, making for a broader array of possible sounds coming
from the instrument.

There was a short motivating lecture around copyright law, which explained the
history of the various extensions to the copyright period covered, along with
how the law works. I learned that this year is the first year that new work
has entered the public domain since 1998, when copyrights were extended by 20
years, thus freezing the public domain for that time.

We then performed are piece, which is based on sample manipulation of musical
works selected from time frames that would place them in the public domain if
older (more liberal) copyright law terms were still in place. We only had about
15 minutes to perform in, after which the students were excused if they needed
to attend the next class, but the faculty and us performers stuck around on
the stage to answer some Q&A. The [Chat](https://github.com/lnihlen/SCLOrkChat)
*exploded* at this time, with everyone feeling the rush of excitement from a
successful performance, combined with the fun intimacy of sharing a private
conversation on stage.

We went to Crepes Place after, a nearby restaurant with tons of tasty
{% include tag_link.html tag="vegan" %} options. I really enjoyed Hilary being
able to finally meet these folks I've been rehearsing with for so long, and
it was fun hearing her share her perspective from the audience with the other
performers.

When I got home I updated the release notes to mark the performance, and pushed
all Quarks forward to version 1.0. It seems only appropriate to consider these
pieces now "in production," given that they have seen actual live use.

It's also liberating to know there's some runway between now and our next
concert. I know that git can protect HEAD with branches, but I also feel more
comfortable introducing new features to the performers with more time before
our next concert, because there's more time to get feedback and iterate on
it, and for everyone to get familiar and stabilize the code before taking it
out for performance again.

So, lots to do! I think there are several quick improvements to the chat due,
and then the longer-term project of the refactor. I'm also thinking of
re-organizing the Quarks into just 2 - one with UI and one supporting the
underlying model code. I had the idea for a window-manager kind of system that
would allow for the different UI elements to tile on top of each other. But
that could also work as a standalone kind of system, that provides a hosting
window if called, or the individual programs can work without.

Stoked!

