---
layout: post
title: Expanding on some ideas
categories:
- Personal
tags: []
status: publish
type: post
published: true
---
A friend of mine has been <a href="http://tickett.wordpress.com/2012/12/31/a-new-year-a-new-project/" target="_blank">thinking about home automation</a> recently, and this got me thinking about a few things but mainly, what would be some good concepts for the infrastructure of such a network of devices.


So whats important?


Easy to set up - technically minded people tend to overlook this aspect or worse yet, misunderstand the true meaning of easy set-up. Wi-Fi pairing is only now becoming a skill that most people are comfortable with, so if we are to have a network of devices that report back to the internet through your home internet connection then we will need to have some very clever programs to enable all this setup with as close to <strong>plug and play</strong> as possible.


Dynamic - any infrastructure is going to have to be able to deal with the dynamic nature of the standard home network/router internet connection. This will be an assign IP to the router and then local assigned IP's for devices within the house


Simple -  If we are going to implement this on embedded devices the concepts have to have a very low overhead for computation &amp; throughput


Proven - As with most things, its probably already been done quite well, so take some of these lessons and build on them.


The underlying functionality of a home automation 'node' is pretty simple, report measurements or switch outputs. The interesting thing comes when we start trying to have a system that can navigate complex network infrastructures (like the whole web, plus the LAN its part of) and report this information back to a server. Maybe we would like the ability to re-route this information to a different server, or multiple outlets.
