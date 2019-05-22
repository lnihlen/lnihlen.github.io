---
layout: post
title: "Parsing Literals in SCLang"
date: 2019-05-22
tags: [ personal, supercollider ]
---

This evening after work I was able to find enough time to report both an
[Issue](https://github.com/supercollider/supercollider/issues/4418) and finish the first draft of the
[PR](https://github.com/supercollider/supercollider/pull/4419) to hopefully improve string to number conversion in the
{% include tag_link.html tag="supercollider" %} language. I encountered this issue in the course of the development of
the parser for SCLang, because I was trying to use these String to Integer and Float methods to validate the parse tree
against the source.

In any event, while I get the impression I'm quite far out in the weeds here for what is supposed to be mostly a music
programming language, the correctness of the Interpreter and support classes (like String) is pretty important to me. I
also understand that with this PR the interruption stack is four deep. At the bottom we start with Scintillator, which
is now sadly beginning to collect some dust once again, interrupted by the idea of the Asset Management system I was
inspired to work on for {% include tag_link.html tag="sclork" %}, which then I got pulled in to some of the formatting
discussion around SuperCollider so I started working on a native Parser interface (making 3 deep), and in the process of
working on that discovered the bug in the number conversion, so now that's number 4.

The cool thing about this interrupt is that since I don't really want to work on the Parser stuff until this fix is
merged I don't feel guilty about putting that work on pause for a few days pending PR review, which gives me a chance to
make some headway on the asset management stuff for SCLOrk. Perhaps my crazy dream of being able to debut some new code
for the orchestra before our Garden of Memory performance will come true after all.

I'm doing my best to not be angry at myself for never even firing up the SC audio server and making sounds with
SuperCollider, outside of the orchestra. This has something to do with the fact that I've decided to accept my creative
self as one that likes to make audio software, and this is just as valid a creative expression as is making audio
itself. I do what I'm motivated to do, pursue what interests me. Outside of work where my responsibilities are to the
company I'm really accountable to noone but myself for how I spend my time. And why would it be that my instincts, which
I trust in most other endeavors, would fail me now?

