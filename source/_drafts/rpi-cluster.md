---
title: Raspberry Pi Cluster
categories:
- Hardware
tags:
- cluster
- rpi
- raspberry pi
---

After I have been playing with docker and experimenting with load balancing applications, moving onto actual hardware seemed like the logical progression.
The main problem with that is cost.  If I did a similar setup with conventional servers as I described in my previous post about docker it would be far more expensive than is feasible for a personal setup.

As luck would have it my interest in embedded computing has provided me with an opportunity to make this setup a lot cheaper with the use of a single board computer called a Raspberry Pi.

![Raspbery Pi Logo](/images/rpi/rpi-logo.png "Raspberry Pi Logo")

Since it's release I have purchased at least one of each type that has been produced and put them for various uses.  

The plan is to re-purpose all of my raspberry pis that are not being used in other projects to make a home cluster for experimenting with.

First I need a way to mount them all in place rather than have them just sat all over the place.  I got a piece of wood that was in my office and proceeded to collecting all my spare Pis and mounting them on in, leaving space between them all to route in USB cables for power and Ethernet cables for wired networking.

![RPi Cluster Board](/images/rpi/cluster-board.jpg "RPi Cluster Board")

This was less than ideal is it is very large, hard to mount the boards to, mostly because it was just a random piece of wood I had.

Networking is also needed for this setup.  In my inventory is a 5 port gigabit switch but I need at least 9 ports if I want to connect all 8 raspberry pis and another port to connect to the router.  I could get an 8 port and drop one pi or get a 16 port for a bit more cost.
This is not what I did.  Instead I took the plunge and bought a 24 port gigabit rackmount switch, under the pretense that it will be used for other projects such as the home made rack.

Slightly less make shift than a piece of wood is my next attempt at mounting all the pis is by using some cardboard packaging and some cable ties.

Cut an amazon box into a square, poked holes in it and strapped the raspberry pis to it by threading cable ties though the holes around the pis.  Also added some extra cable ties in as runs for the networking cable to keep it out of the way.
The card was cut to fit in a rackmount drawer which was previously occupied by a laptop.

![Rackmount Drawer](/images/rpi/rack-drawer.jpg "Rackmount Drawer")

Featured in the picture is also an 8 port USB power supply in the top left corner. This is handy because it is a single cable into the drawer to power all of the Pis.  Also you may notice there is only 6 pis in the drawer, this is for 2 reasons:

- The RPi Zeros need an external ethernet adapter with takes up space due to the length of the cable.
- I wanted to keep the Zeros for other projects when they can be embedded such as some home automation applications.

Running the networking cables around the edge of the drawer (mostly) and out the back worked out well.  It allows the drawer to still function.  They come out the back, loop around to the front of the rack and into the switch.  The switch now blinks like crazy when using the pis as there are 2 lights per connected device.

Here is what the rack looks like with all of the pis in the drawer, connected up and powered on.

![RPi Rack](/images/rpi/rpi-rack.jpg "RPi Rack")

This could be made much smaller but I wanted it to fit into the rack that is under construction in my house.  May as well put everything in one place.
