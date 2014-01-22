---
layout: post
title: Cloud9 & RasPi Pt2
categories:
- Node.js
- RaspberryPi
tags: []
status: publish
type: post
published: true
---
[Cloud9 &amp; RaspberryPi](http://chrismatheson.github.io/2012/10/17/cloud9-raspberrypi/): After completely blowing away my SD card i created another one this time installing Node 0.8.1 with [these instructions](http://www.raspberrypi.org/phpBB3/viewtopic.php?f=34&amp;t=18775) and source mint installs with no problems at all.

On-to the next problem, libxml. libxml is an npm package which i believe wraps the libxml Debian package with node bindings. There is a flag set in the build command line '-msse2' which is incompatible with the ARM architecture, this is known about but not yet fixed [https://github.com/ajaxorg/node-libxml/issues/7](https://github.com/ajaxorg/node-libxml/issues/7)

so to counter this i think i have to try and build libxml beforehand and then run the cloud9 install scrip again.

[StackEx conversation](http://raspberrypi.stackexchange.com/questions/3348/how-do-i-install-libxml-on-raspbian)
