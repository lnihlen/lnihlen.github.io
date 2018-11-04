---
layout: post
title: "Continuity"
date: 2018-11-03
tags: [ personal ]
---

An "active recovery" day from the work week. We watched a few more movies from
the Lynda Thompson project, up through Poltergeist II. Because I had messed up
the groups on my lone user account on the laptop, and because I didn't have
root password, I decided that was sufficient impetus to try and put Gentoo on
the System-76 Oryx. Oh, their new open-source desktops,
[Thelio](https://system76.com/desktops) look amazing, BTW. Next workstation I'm
thinking of buying is likely to be one of those.

So yeah, got X building but it won't start. First there seemed some permissions
errors, unable to access `/dev/ttys0`, but now it can't create a virtual
display. I'm wondering if there's some issue around the dual video cards on the
laptop, but nothing I'm reading via Google search seems to point to that
especially.

I might abandon this and go back to Pop! OS. It's not that its bad, honestly I
think I put Gentoo on stuff because I think the install process is fun. But
laptops serve a practical need for me, and I'm not sure I want to spend the
time to get this one up to the level of sophisticated behavior you seem to
be able to get out of the box by installing their own flavor of Linux.

The Rabbids Kingdom Battle game is getting hard enough that it's not as fun, I
find myself having to replay missions and spend a lot of time min/maxing the
different characters and loadouts to try and just survive a fight.

Been thinking a bit about {% include tag_link.html tag="vcsmc" %} again, if I'm
honest. I'm stuck re-working the
[CIEDE2000](https://en.wikipedia.org/wiki/Color_difference#CIEDE2000) color
distance calculation into Halide. It's a long calculation with a lot of math and
a ton of intermediate variables. All of the Halide examples and documentation I
can find use very short calculations, like the sum of the inputs. The most
sophisticated example I can find is a 2-part blur. Perhaps multiple `Exprs`
could be combined though? Worth a thought, by which I mean "worth a lengthy
and confusing struggle with the compiler."

