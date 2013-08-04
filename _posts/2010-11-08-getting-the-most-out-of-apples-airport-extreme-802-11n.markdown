---
author: admin
comments: true
date: 2010-11-08 04:00:33+00:00
layout: post
slug: getting-the-most-out-of-apples-airport-extreme-802-11n
title: Getting the most out of Apple’s Airport Extreme and other 802.11n routers
wordpress_id: 163
---

WiFi is nowadays as ubiquitous as email, cell phones, or mp3 players. And as each new WiFi technology has come up, we've been able to use the technology, ironically, to "wire" our homes with all kinds of media and connectivity.

802.11b, the original standard with mainstream success, was good enough for web browsing but not much more. Its successor, 802.11g, has been good enough for web browsing and streaming most kinds of video, and is still the most commonly deployed standard in today's home routers and mobile devices (including smartphones).

But newer 802.11n standard routers are available this year (and supported on most new laptop models) that allow you to reliably stream blu-ray quality HD video anywhere in your home (with a strong enough signal permitting). But to get the sort of reliable throughput you expect for uninterrupted HD video streaming, a few tweaks need to be made.

Enter Apple's [Airport Extreme](http://www.apple.com/airportextreme/).

Apple's gear is generally quite good, made from quality parts, and speedy out of the box. But as a consequence of how 802.11 networking works, you can make a few tweaks to the Airport Extreme configuration to get extra speeds.

802.11b and g traditionally ran on 2.4GHz networks. But 802.11n added 5GHz to its operating frequency. Unlike the 2.4GHz band, 5GHz offers much less interference, at least for now, only because there are much fewer devices that run on them. But this ability also gives wifi routes additional power to run at much higher speeds.

However, for maximizing backwards compatibility, if there are any 802.11b/g devices on the N network, the router kicks back into G mode, and runs on G speeds. To get the most out of your N network, you need to run a separate network purely for N devices.

Since you are running a network on N devices, and since all N devices support 5GHz, why not run it on 5GHz? This is exactly what the Airport Extreme gives you, but in a very non-obvious way.

Note below the transfer speeds I measured from transferring a 1GB video file across the G, N (2.4ghz) and N (5GHz) network:

File Size: 1.01 GB h.264 video

Sharing using the AFP protocol between a Mac Mini (source) and Macbook Pro (destination) 8 feet away in the same room:

802.11g at 2.4 GHz: 769 seconds

802.11n at 2.4 GHz: 467 seconds

802.11n at 5 GHz: 209 seconds

The huge difference in running on a pure 5 GHz network is worth the upgrade to a good 802.11n router. The Airport Extreme allows you to run two networks (one hybrid, one pure 5 GHz). Definitely exercise this option so your N devices can run on their own network and get the huge (100%+ speedup) benefits.
