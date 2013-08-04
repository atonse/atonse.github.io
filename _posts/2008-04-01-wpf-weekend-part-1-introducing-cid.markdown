---
author: Ashish
comments: true
date: 2008-04-01 01:02:13+00:00
layout: post
slug: wpf-weekend-part-1-introducing-cid
title: 'WPF Weekend, Part 1: Introducing CID'
wordpress_id: 15
categories:
- Misc
tags:
- csharp
- dotnet
- microsoft
- wpf
---

Over lunch with my friends at [OpenSource Connections](http://www.opensourceconnections.com/) last Friday, we had a discussion of how they could attract more people to their booth at the FOSE convention next week in Washington, DC. A recurring suggestion was to have something to dazzle people from a distance.One of the ideas we came up with is to have an eye-catching display, but that only had limited value.

So we decided to show attendees information that is immediately useful to them, such as the conference event schedule.SO this weekend, Michael Herndon from OSC, and myself, started to build what would become CID.

We decided from the beginning to open source the project and host it on Google Code, so that others can benefit and learn from our experience, and also so that it could be extended easily in the future. This series of posts outlines some of the things we learned in the process.

<!-- more -->


### WPF


Firstly, a short intro to WPF. WPF is short for Windows Presentation Foundation, is a set of Microsoft-based technologies (namely, XAML and a .NET 3.0 Presentation Framework) that allow developers to build rich media applications which take advantage of graphics hardware that’s common in today’s computers. For a better overview of WPF, go to [WPF](http://en.wikipedia.org/wiki/WPF).


### Goals


There were three goals to this project:



	
  * Bring people to the OSC Booth and make them talk about it

	
  * Show off OSC’s skills in cutting edge technologies (like WPF)

	
  * And most importantly, it gave us an excuse to play with WPF. ;-)




### Tools we used


Not much of a surprise, but we used entirely Microsoft-based tools, since they were optimized for building WPF applications and writing XAML.- [Visual Studio 2008](http://msdn.microsoft.com/vstudio/) (with [.NET 3.5](http://www.microsoft.com/downloads/details.aspx?FamilyID=333325FD-AE52-4E35-B531-508D977D32A6))- [Expression Blend 2 February CTP](http://blogs.msdn.com/expression/archive/2006/02/22/537105.aspx)


### The App


[![cid-small.jpg](http://ashish.tonse.com/wp-content/uploads/2008/03/cid-small.jpg)](http://ashish.tonse.com/wp-content/uploads/2008/03/cid-screenshot.jpg)[](http://ashish.tonse.com/wp-content/uploads/2008/03/cid-screenshot.jpg)

Click above for a screenshot of the final app (final as of this weekend). In the coming days, I’m going to outline how we did various things with CID and WPF. I want to cover the following topics:



	
  * Part 2: Layouts

	
  * Part 3: Databinding (Relative, Elements, DataContexts)

	
  * Part 4: Animations, Per-character Text Effects, Calling Storyboards from C#

	
  * Part 5: Code-behind events, programmatic animations and storyboards, and wrap-up 


So stick around! :-)
