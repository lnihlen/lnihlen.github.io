---
layout: post
title: "Gentoo on My Old System"
date: 2018-09-27
tags: [ personal ]
---

I have a crusty old Gentoo box that's in hard use at home. It went down this
morning and so when I got home I started poking at it to try and revive. After
a therapeutic reboot I noticed that it hadn't been updated in quite some time.
After an `emerge --sync --quiet` I ended up in a fun chicken/egg situation where
the version of `portage` that I had installed provides `EAPI 6`, but one of the
dependencies of the new version of `portage`, specifically `pinentry`, requires
`EAPI 7`. So, in other words, the tool to install the thing requires a newer
version of the tool to install the thing.

The answer, after an hour or so of tinkering and a lot of googling around, was
to use an `emerge --nodeps portage` command to force the `portage` package to
install without pulling in the broken dependency. That worked.

Then it was a coupla iterations of `emerge -uaD @world` with a few addenda to
the `package.use` to resolve masking confusion it looks like I'm off to the
races with probably another all-night rebuild, starting with `glibc`, which
is usually a good sign.

TV show of the night is
[Insecure](https://en.wikipedia.org/wiki/Insecure_%28TV_series%29). This is a
Hilary pick but I got sucked right in. Issa Rae is incredible, the characters
are compelling and human. It's super good.

