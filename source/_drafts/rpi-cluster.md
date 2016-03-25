---
title: Raspberry Pi Cluster - Part 1
categories:
- Hardware
tags:
- cluster
- rpi
- raspberry pi
---

After I have been [playing with docker](/2016/03/24/docker/) and experimenting with load balancing applications, moving onto actual hardware seemed like the logical progression.
The main problem with that is cost.  If I did a similar setup with conventional servers as I described in my previous post about docker it would be far more expensive than is feasible for a personal setup.

One of the smaller general purpose computers I could find was a little [intel celeron box](http://www.novatech.co.uk/pc/range/novatechpockithdnpi17.html) as it is very small and cheaper than a large tower.  They are £165 each so having a setup described in the docker post (1x load balancer, 2x applications, 2x database) would require 5 of them, totaling at £825.

As luck would have it my interest in embedded computing has provided me with an opportunity to make this setup a lot cheaper with the use of a single board computer called a [Raspberry Pi](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) which costs just £30.

![Raspbery Pi Logo](/images/rpi/rpi-logo.png "Raspberry Pi Logo")

Since it's release I have purchased at least one of each type that has been produced and put them for various uses.  

The plan is to re-purpose all of my raspberry pis that are not being used in other projects to make a home cluster for experimenting with.

First I need a way to mount them all in place rather than have them just sat all over the place.  I got a piece of wood that was in my office and proceeded to collecting all my spare Pis and mounting them on in, leaving space between them all to route in USB cables for power and Ethernet cables for wired networking.

![RPi Cluster Board](/images/rpi/cluster-board.jpg "RPi Cluster Board")

This was less than ideal because is it is very large and hard to mount the boards to; mostly because it was just a random piece of wood I had.

Networking is also needed for this setup.  In my inventory is a 5 port gigabit switch but I need at least 9 ports if I want to connect all 8 raspberry pis and another port to connect to the router.  I could get an 8 port and drop one pi or get a 16 port for a bit more cost.
This is not what I did.  Instead I took the plunge and bought a 24 port gigabit rackmount switch, under the pretense that it will be used for other projects such as the [home made rack](/2016/03/23/servers/).

Slightly less make shift than a piece of wood is my next attempt at mounting all the pis is by using some cardboard packaging and some cable ties.

I cut an amazon box into a square, poked holes in it and strapped the raspberry pis to it by threading cable ties though the holes around the pis.  I also added some extra cable ties in as runs for the networking cable to keep it out of the way.
The card was cut to fit in a rackmount drawer which was previously occupied by a laptop.  This has 16" x 14" of usable space inside.

![Rackmount Drawer](/images/rpi/rack-drawer.jpg "Rackmount Drawer")

Featured in the picture is also an 8 port USB power supply in the top left corner. This is handy because it is a single cable into the drawer to power all of the RPis.  You may also you may notice there are only 6 RPis in the drawer, this is for 2 reasons:

- The RPi Zeros need an external ethernet adapter with takes up space due to the length of the cable.
- I wanted to keep the Zeros for other projects when they can be embedded such as some home automation applications.

Because I already had all of the raspberry pis it did not cost me anything to put them into this project but if you were buying them all new and went with the latest model for all 6 it would cost about £180.  Around the cost of one new low end desktop.

Running the networking cables around the edge of the drawer (mostly) and out the back worked out well because it allows the drawer to still function.  They come out the back, loop around to the front of the rack and into the switch.  The switch now blinks like crazy when using the RPis as there are 2 lights per connected device.

Here is what the rack looks like with all of the RPis in the drawer, connected up and powered on.

![RPi Rack](/images/rpi/rpi-rack.jpg "RPi Rack")

This could be made much smaller but I wanted it to fit into the rack that is under construction in my house.  May as well put everything in one place.
