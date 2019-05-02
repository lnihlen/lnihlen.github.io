---
layout: post
title: "Slow Waves"
date: 2019-05-01
tags: [ personal, sclork ]
---

Going through routine at work, letting the last few days just kind of spool out. I'm back-to-back every day now, in
fact have a meeting every half hour from 8 am tomorrow until 5 pm. So there's not even really time for me to take the
early meeting from home, then sneak in to work. It'll be one of those days where I have to pick which meetings I'm
going to be late to for things like going to the bathroom or grabbing lunch.

In the meantime there are slow waves of emotion going through me around the last performance review. I can gauge the
progress of the wave by my levels of psychological safety, defensiveness, ability to be present for others. But in
less than 48 hours now it will all be over, so that's something.

This evening tried to get a better understanding of move semantics, which somehow seem both mysterious and also totally
mundane. Hoping for more of the latter and less of the former. Also I'm digging in a bit to reading Effective Modern
C++, although I find (like the old ones) I have to read the points very much out of order so that I can even understand
them.

Made a bit of progress on the Database object within confab for {% include tag_link.html tag="sclork" %}. With the
introduction of flatbuffers I wanted a way to return pointers to internal memory within LevelDB without copies, but
to make sure that internal memory gets reclaimed when the caller doesn't need any more of it. So something like a
```std::unique_ptr<T>``` but where the destructor instead deletes a ```LevelDB::Iterator```. After a long time of
wrestling with the compiler I found a
[helpful article](https://www.cprogramming.com/c++11/rvalue-references-and-move-semantics-in-c++11.html) that made me
realize I needed to implement a move constructor.

I still haven't picked up the habit of using ```auto```, though. Not sure what that's going to take. Maybe going through
and refactoring everything I've already written to aggressively use it? There's some serious muscle memory here. I can
type:

```
for (int i = 0; i < something; ++i) {
}
```

about as fast as any English word. And changing from ```i++``` to ```++i``` took a looong time, and I was a much younger
man. So maybe I can turn that ```int``` into ```auto```, it's just gonna take some time.

As always, ever more shall be revealed.

