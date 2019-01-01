---
layout: post
title: "SCLOrk Quark Bork Bork"
date: 2018-12-31
tags: [ personal, sclork ]
---

Hil and I took the dogs to the beach this morning. It was a beautiful day, the
sun was shining even if the wind was a bit cold. There were few enough people
on the beach that we let the dogs off leash for a while and they ran wild,
doing laps around us and having fun.

Then it was time to knuckle down on some more of the
{% include tag_link.html tag="sclork" %} work, as tomorrow is the day when I'm
going to be hoping to drop off working versions of everything to Bruno for
use in the student-driven rehearsals that I won't be able to attend.

I made good progress on the server, including writing my first Gentoo
initscript to launch both the chat and the clock server objects after system
bootup, which is pretty cool. I might even be able to set up an init script
that will try to pull the latest version of the repository before attempting
to run the script.

In any event, things were going smoothly until I started trying to test the
"production" alpha versions of my Quarks, by uninstalling the directories I've
been developing from and trying to provide GitHub URLs to the Quarks interface
to make them pick up the release versions.

I build my SuperCollider from source, so maybe production versions aren't
having this issue, but the
`Quarks.install("https://github.com/lnihlen/SCLOrkChat");` command that
was working literally yesterday today is failing with a weird
`path doesn't exist` error.

Perhaps things are confounded by the fact that I broke some of the objects in
both SCLOrkChat and SCLOrkClock into a separate Quark, one with no UI
dependencies, called SCLOrkNet. Then I added SCLOrkNet as a dependency for
both of the other Quarks. It may be that the dependency part doesn't like the
path I'm providing, or perhaps the syntax of the path was funny, but things
were getting seriously weird on multiple machines that I was trying to test
on.

So I've reset my Quarks to default, made a PR to add my Quarks to the official
list, and did a final release on each Quark that presumes it is in the official
list and so therefore can be referred to only by name. My hope is that when
the PR gets approved installing these Quarks can be as simple as picking them
out from the list. Of course, about an hour after submitting I realized I just
created a PR on an open-source project during the middle of a near-global
holiday. So maybe odds are good it will sit for a few days, which is fine.

I'm definitely anticipating there will be further work on all of these, they
need a bunch of polish. But looking back over this break I am proud, I've done
a *ton* of work, and there's a reasonable chance that some of this code could
even be useful.

Happy New Year!

