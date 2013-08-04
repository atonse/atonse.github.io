---
author: Ashish
comments: true
date: 2008-04-06 10:19:17+00:00
layout: post
slug: googles-app-engine-platform
title: Google's App Engine platform
wordpress_id: 17
categories:
- Misc
tags:
- app-engine
- google
- python
---

This evening, Google unveiled something called the App Engine:




	
  * hosting environment exclusively for web applications

	
  * initially free up to a certain site load (500 MB storage, 10 Gb bandwidth a day, ~5 million pageviews/month -- I wish that was a problem I had!)

	
  * supports Python (initially) but will eventually support more languages

	
  * they seem to have their own api and their own web application framework, I wonder if they'll support more like Django (Python) or, of course, Ruby on Rails :-)



How this compares to Amazon:

	
  * This is not a general purpose web hosting or grid service like EC2 -- this is tailored specifically to web applications

	
  * Free up to a certain amount of usage (probably only something Google/MS could afford to offer)




<!-- more -->



### My Thoughts


The main thing that struck me at first was that it was based off Python. Not a surprise because Google is pretty much the largest promoter/user of Python on the internet, they even hired Python creator Guido Von Rossum. But apparently from the talk, Python is only the first supported language. More will be added over time.

The other thing that struck me was that they seem to have chosen to develop their own web application framework. I wonder why. There are plenty of good ones out there (like Django for Python). I hope this isn't just a case of programmers always wanting to implement their own version of a certain app just for problem-solving satisfcation and the joy of learning something new.

But again, if they allow other languages to be supported, I'm sure they'll eventually allow various frameworks. If I had to guess, I'd think their framework probably handles caching and database persistence really well with their backend, which makes it the most ideal. But knowing Google, they will probably open up all the protocols being used to interact with their infrastructure, and allow the community to develop mappings in other languages. Nothing wrong with this inherently open source approach.

The final thing to note is that this is a preview release, and a lot of my worries will most likely be put to rest by the time they release a final version.

This is quite promising for developers. These are very interesting times for small companies. It is growing ever easier and cheaper to have an IT infrastructure that supports more and more users. There are startups that run entirely on Amazon S3 and EC2, and don't own a single server. This is just possible because of the internet and a lot of its supporting technologies becoming cheaper.

Now that I think about it, it's actually a very Apple-like approach to this problem. We give you the whole ecosystem where all the pieces work together perfectly, and as long as you use our tools and technologies, your app will work beautifully. It has limited appeal.

Now I'm waiting for Yahoo and Microsoft's reponses :-) They better be working on something worthwhile to compete. This is the future of startups.

Overall, I think Amazon is still king of this space. This thing got a luke-warm reception from myself (and apparently most who attended). Hopefully it'll mature into something more useful for a larger number of people.
