---
layout: post
title: "Long Way 'Round"
date: 2019-05-23
tags: [ personal, sclork ]
---

It's very late because I got distracted in building a Trie to support efficient linear searching for emoji by keyword. I
had switched gears back to working on the {% include tag_link.html tag="sclork" %} code, with the express goal of
building in support for emoji in the chat by building out a complex asset management system. Of course, staring me right
in the face this whole time has been the SuperCollider [String documentation](http://doc.sccode.org/Classes/String.html)
which mentions in the front matter that Strings have support for UTF-8, including emoji.

I copypasted some UTF-8 characters into the editor for insertion into different UI elements in the chat and of course
they worked just fine. So... been building a whole complex C++-based asset sharing system and it turns out the first
goal I had envisioned for that system, emoji support, has a much more trivial solution.

It was off to the Wnicode website then to download a
[current list of emoji](https://unicode.org/Public/emoji/12.0/emoji-test.txt), including descriptions and code points.
And although I had an overlong day at work and little time to work on this I was still able to write a script for
SCLOrkTools that takes that list and breaks it out into a Trie in the form of a MultiLevelIdentityDictionary, an oddity
of a data structure inside of SCLang that I've been itching to get a bit more experience with anyway.

I think I have the thing running now, and tomorrow my attention can turn towards building the UI for supporting emoji
search by keyword and insertion into the chat text entry window. But for tonight, it's way too late, got another full
workday tomorrow followed by an international flight on Saturday, so I will close for now.

