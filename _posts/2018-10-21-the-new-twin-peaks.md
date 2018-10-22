---
layout: post
title: "The New Twin Peaks"
date: 2018-10-21
tags: [ personal ]
---

Spent the night in the pop-up camper, for the first time, while it was parked
in the driveway. I'd say the mattress is a little thinner and harder than I
would entirely like but it beats hell out of sleeping on the ground. The evening
was without incident, which I took to be a good sign. I'm starting to get pretty
excited about taking it out for an actual camping trip next weekend.

Then it was time to tackle something that I've been dreading ever since picking
the camper up in Salinas, the loading of the pop-up into the truck. There's
very little tolerance on either side of the camper and the walls of the truck.
When I had first picked it up some folks at the dealership loaded it for me,
and I had noticed how sketchy that seemed even for them. Given also that Hilary
is out of town I knew I would have to attempt it alone.

I think end to end I spent about an hour prepping the trailer, backing the truck
carefully under it, lowering the trailer in to the bed, and attaching the camper
to the truck. I had to re-raise the trailer to shimmy the truck over a bit in
order to make the attachments line up well enough to not dent the side of the
truck. And I think there's probably some additional scraping along the side
of the camper, right along where the guys loading the camper at the dealership
also scraped it a bit. They assured me that it was not a big deal and I
certainly hope they're right because there's more there now than before.

![camper loaded in truck]({{ "assets/img/blog/2018-10-21-1.png" | absolute_url }})

But, all said and done, and I loaded it up. I'm hoping that all I have to do
before leaving is flush the water out of the camper and replace it with new
water, because the stuff in there right now tastes terrible. Probably worth
considering winterizing the camper once I return, unless I decide that some
winter camping might be in order. Cool thing about this camper, with built-in
heater, is that I really have the option of camping year-round. Once things turn
colder I imagine that most of the campsites that are still open will thin out
pretty well, giving myself (and possibly Hilary) some privacy.

So yeah, pretty excited. Think next weekend will be fun.

On the {% include tag_link.html tag="sclork" %} front I picked up the fanless
rackmount server yesterday and racked it along with the ethernet switch. I
put Gentoo on the server and got at least the DHCP service working. There's some
issues with the NAT and firewall stuff I had in place, I can't seem to get it
to route the traffic from the LAN to the WAN appropriately. There may be some
kernel config that I'm missing, I went through a bunch of kernel config stuff
back in the day when I was building my own router, but it seems like the options
have changed. I might be missing something. Next time I take a crack at it I
think I'll look at the router config and see if I can spot some obvious
difference.

I got NFS working on it, so we can at least enable file sharing when the group
gets together.

Was nice to see the PXE boot options in the dnsmasq config file, I'm looking
forward to being able to play with those to get the Pis going. I have them
built and sitting on top of my rack, like so:

![Pi cluster on top of rack]({{ "assets/img/blog/2018-10-21-2.png" | absolute_url }})

You can see a frame from the new Twin Peaks playing on the TV in the background.
I have to say, re-watching it I think the show makes more sense, and I'm
enjoying it more this time around.

Remaining work I'm hoping to have fixed up before next SCLOrk rehearsal:

  * Get an initial draft of the chat application going. I have some UI rendering
    going, and initial logic in place, but lots more here to do. I'm hoping I
    might be able to tackle some of this while camping, with some peace and
    quiet (and no/limited distracting Internet connectivity).
  * Fixup the NAT/forwarding stuff on the fanless server. This is less about
    performance capabilities for SCLOrk and more about correct configuration of
    my hardware, and allowing devices on the subnet (such as the MOTU 16A) to
    see an Internet connection if there is one.
  * (Stretch) make some headway on connecting the server to the MOTU so that it
    can do multitrack recording, as another step towards the PXE-booted Pi
    array setup for Utopia BeaconClock research.

