---
layout: post
title: "Named Assets"
date: 2019-08-01
tags: [ personal, sclork ]
---

This morning's working session yielded up almost a complete implementation of named asset support for the
{% include tag_link.html tag="sclork" %} asset sharing system. I got almost all the parts of it working except for the
actual SuperCollider language support, which usually codes up pretty fast. Now that I have bits flowing from sclang to
client to server and back, it's a bit easier to add additional signals to the existing pathways. It's definitely
satisfying to be able to sit down and bang out a satisfying chunk of work like that.

There already was a ```name``` field iun the Asset metadata, so the first move was to add logic to store a reference
back to the Asset under that supplied name. This meant I spent a minute extending LevelDB's support for atomic batch
writes to the exterior Then I was able to add pathways to retrieve Asset metadata by name. There
are still some open questions around Asset deprecation and how that works with replacing an older Asset with the same
name with a newer one.

A bit more on this and then I'm ready to get a first crack at lists. I think with a rough implementation at both I can
turn my attention back to the chat system and rebuild it using these Asset system features. Feeling a bit like a broken
record on this but I call it *focused.*

