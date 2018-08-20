---
layout: post
title: "Tap Tempo Sequencer"
date: 2018-08-19
tags: [ supercollider, oort_cloud, i_made_a_thing ]
---

Another chance to sleep late, this time in our own bed, and then up with Hilary
to make some {% include tag_link.html tag="vegan" %} pancakes and waffles,
along with some seitan strips cut thin and sauteed to be like bacon.

The band was coming over in the afternoon for a practice so I spent some time
trying to make progress on the tap tempo sequencer that I've been working on
in {% include tag_link.html tag="supercollider" %}. A bit ago I took an awesome
[week-long workshop](https://ccrma.stanford.edu/workshops/supercollider-2018)
on supercollider at [CCRMA](https://ccrma.stanford.edu/). Each student picked a
final project and worked on it for most of the week, with the support of the
faculty coordinators Bruno Ruviaro and Fernando Lopez-Lezcano.

It was a real treat to take a week and hack on SC, in such a prestigious and
supportive environment as CCRMA. For my final project I chose to focus on
building a system that could accompany my band on bass synth while we perform.

I play drums and the guitarist normally leads us in, to almost every song. Once
Grawer starts playing the hook I pick up the tempo from that, and then come in
with the drums. My plan was to build a tap tempo system using a MIDI foot
controller, and have that drive a
[Moog Minitaur](https://www.moogmusic.com/products/taurus/minitaur). For the
foot controller I selected a
[Roland FC-300](https://www.roland.com/us/products/fc-300/) so that I could use
the two foot pedals for both a cue volume (for my in-ear monitors) and a mains
volume, and have enough other switches that I could tap a tempo out, control
song start, stop, and reset, and pick the active song from the set list.

During the week of the supercollider workshop I wrote a rudimentary tap tempo
controller, figured out how to get MIDI output working to drive a software synth
(the Minitaur took its time getting to me in the mail), and got some preliminary
song switching and setlist programming in place. I built a small UI, mostly
showing status indicators, and figured I might get SC running on a Raspberry
Pi with touchscreen, so I wouldn't have to haul my laptop to gigs. By Thursday
of the workshop week I had
enough of the system put together I could start testing it, and that's when I
discovered that the tap tempo thing I had built was almost completely
unworkable. I was trying to play along with a live recording of us and found
that while I could match the tempo accurately by computing the mean period
between taps on the foot controller, I had a hell of a time synchronizing that
with the individual beats of the performance.

The challenge is that when another musician is tapping out a lead-in, for
example envision a drummer hitting their sticks together on a four count before
the start of a song, is that two pieces of information are being relayed by
the tapping at the same time. My first draft of the tempo system only accounted
for tempo, by measuring the time between taps and computing a rolling average
of those tap periods. The other, and arguably more important datum from the
tapping is *synchronization*, which from a tempo perspective can be considered
as phase.

The second revision,
[committed here](https://github.com/lnihlen/sc/blob/d1c9ed5fca07ea7ce5bb764cc6e2814fd709c874/classes/TapStreamPlayer.sc),
tracks enough taps from the input to get an accurate period mean, but is also
ready at any time to schedule the next beat for immediate playback if a tap
comes in early. I confess I haven't tried it in full equipment setup, but the
[test rig](https://github.com/lnihlen/sc/blob/00949143b101d39ede1d729e0d32d6f3f0b9e310/tap_stream_player.scd) I built for laptop hacking has the feeling of
an unstable system working at cross-purposes.

The root of the problem is that it is currently not possible for the system
to determine when it should *lead*, by scheduling the music based on the tempo
estimated from the taps, or *follow*, by waiting for a tap to come in and only
moving forward in the score from tap to tap. So, it attempts to do both at
once, scheduling a beat at a time but allowing incoming taps to preempt the
next scheduled beat, with some awkward heuristics around trying to determine
if an incoming tap was intended to be the previous tap late or the next tap
early.

I'm thinking of a subsequent revision to the system that would require me to
be explicit in mode change from lead to follow or back. The system would start
in follow mode, tracking the tap button to get a tempo, but not playing the
melody. Then I would hit another button to start the melody on lead mode, which
will play the melody along the established tap tempo. Playback will continue
in a loop until the tap button is hit again, at which point the system will
fire any scheduled events but not schedule any new ones, and will wait until
each manual tap comes in to fire one beats worth of events.

There still is the need to advance the music one beat at a time, so any
subdivision of the beat has to schedule all events during that beat based on
the measurement of the historical tempo. What this means in practice is that
there is no smooth *retardando* or *accelerando*. But perhaps that could be
another purpose for one of the foot pedals at some point, if the band comes
up with riffs that go through some tempo changes.

But the realities of the day job loom, it's perf season at work, and I imagine
my available free time rapidly shrinking to nothing for the forseeable future.
So perhaps these are notes for my future self when I emerge blinking from that
time sink a few months hence.
