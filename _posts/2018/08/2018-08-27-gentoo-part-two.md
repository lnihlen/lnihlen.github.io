---
layout: post
title: "A (staggeringly less productive) Monday of Gentoo"
date: 2018-08-27
tags: [ i_made_a_thing, personal ]
---

Day two of the Gentoo workstation journey. Booted to the install disk again and
started mulling the idea of nuking the partitions and starting the install
process over from scratch. Figured it'd go a lot faster this time, particularly
if I copied the ```make.conf``` or at least the ```USE``` flags from inside it.

But that got me to thinking that I hadn't tried hard enough to unwedge my
current install. Used the handy-dandy
[Gentoo cheat sheet](https://wiki.gentoo.org/wiki/Gentoo_Cheat_Sheet) to
selectively unmerge all of the ```X```-related targets in the ```world``` file,
and then several more, until ```emerge``` was willing to do a ```depclean```.

That meant I was back to a bare-earth install of gentoo with no ```X``` support
at all installed or configured, but unwedged at least. So, I kicked off the
```emerge xorg-server``` and headed to work.

Busy day at the Googleplex but I did manage to grab a minute over lunch to go
over the [long list](https://wiki.archlinux.org/index.php/window_manager) of
options for window managers again over on the Arch Linux site. I settled on
bspwm.

Then I get home, go through the (quick) install/build cycle for bspwm, and just
trying to get a usable work environment configured I burn through the
(complete lack of) documentation and find myself reading example configuration
files on github.

I thought the whole point of these minimalist window managers is that they will
*get out of your way* and let you get to the work, so why is it I have to
drag up my dusty memories of Lua, of all things, just to get a desktop that
can launch a terminal?

So I'm about 2/3 of the way through a
[Plasma Desktop](https://www.kde.org/plasma-desktop) install. I think that's
maybe a part of being a technology worker *of a certain age*, in that I am
more than happy to tolerate a bit of bloat in my distro if it means I don't
have to spend a few hours Googling around to get to a desktop with terminal,
gVim, and Chrome. The compromise of the youthful idealistic standards. There's
bloatware and proprietary drivers on my largely-built-from-source workstation.

Maybe tomorrow's entry will be typed on the new workstation! One can only hope.

