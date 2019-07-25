---
layout: post
title: "First Deep Working Experiment"
date: 2019-07-24
tags: [ personal ]
---

So I was up early to try 90 minutes of deep work, following the [Deep Work](http://www.calnewport.com/books/deep-work/)
book I've been raving about. This is email and Slack windows closed, didn't even play music, focusing on working on the
next piece of code for {% include tag_link.html tag="sclork" %} asset sharing system. It's difficult to say exactly how
"deep" I went, and of course I feel like I probably could have gotten a great deal more code written, but I did manage
to write a substantial portion of the file cache, which is the way the client is now planned to handle caching assets.
I like having the file cache because it doesn't duplicate the storage cost of larger assets by keeping them both in the
database and in the cache. It was a fun opportunity to use a bit more of the ```std::filesystem``` stuff, new to C++,
and pretty awesome to use, although it seems the spec tightens up nicely in C++20.

It's clear that there's obvious value in this, and also clear it's going to take some time to calibrate and tune all of
the processess to support truly deep working sessions. A lot of the advice in the book seems to be about structuring
one's life to aid in productive, creative output. I can get behind that. I feel that my life has moved towards a real
*lack* of focus in recent years, particularly with my move to management, which fragments my time in the day to half
hour segments. There's never enough time to really dig in to issues in a half hour, I think, and so it keeps me in the
shallows.

I'm also thinking more about this blog. I think I ended up with a personal goal of writing a blog post every single day
consistently for a year. I'm about 3 weeks away from meeting that goal, and I want to complete it. I don't have
analytics set up here or anything, I think I've been writing to myself more than anything else, it just happens to be on
the Internet. I'd be deeply deeply surprised if average readers per week is even a fraction above 1 person, that person
being me checking that the article rendered alright. Aside from any tools of measuring engagement, I can look back on
probably the vast majority of the postings on the blog and assume that they are of little interest to individuals beyond
myself.

But, in an effort to refocus more of my time on working deeply, I'm thinking of restructuring the blog to focus on
longer-form articles. It feels good to work on my writing a little bit each day. What I think I've observed is that I
don't have the time on a single day to really produce the kind of value in a written artifact that might be worth
somebody's time and attention. Substance, *depth*, takes time and deep work. So I think that's the direction I'd like to
move this.

But first I'll finish those three weeks out. I'm just going to take this time before the year milestone to practice
focusing more on writing these entries, perhaps treating it as a warmup.

