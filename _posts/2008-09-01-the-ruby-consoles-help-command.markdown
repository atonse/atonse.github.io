---
author: Ashish
comments: true
date: 2008-09-01 23:11:10+00:00
layout: post
slug: the-ruby-consoles-help-command
title: The Ruby Console's help() command
wordpress_id: 44
tags:
- docs
- irb
- ruby
---

I am writing this blog post offline on my flight to Austin via Atlanta. I am working on a Rails application and I needed to look at the different methods available for ruby Arrays. And I didn't take an offline copy of the Rails or Ruby documentation. But I thought that perhaps Ruby would have something similar to Python's dir() command, which is essentially a function in the python console that returns a list of possible functions and meta information for a given type.

<!-- more -->

So for example, if you did the following in the Python console:

`
>>> a = ['a']
>>> dir(a)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__delslice__', '__doc__', '__eq__', '__ge__', '__getattribute__', '__getitem__', '__getslice__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__setslice__', '__str__', 'append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
`

As you can see, the object 'a' is an array. And when I type dir(a), the python console returns the properties available to a Python Array object. It's an extremely useful way of discovering the features of the languages, especially when you just like tinkering.

It turns out (and I didn't know this) that there's a similar command in the Ruby interative console, help(). This basically allows you to look up the documentation for base classes and features of the given class. So you can do the following (slightly different from Python):

`
>> help(Array)
`

Ruby sends you to a text page similar to a *nix man (manual) page. This works on the class level and also the class method level, such as:

`
>> help('Array.delete')
`

Note that when mentioning a method for a class, you must enclose it in quotes, or it won't be able to find it in help. It's not necessary to enclose a class lookup in quotes though. This is a really useful command for people who are stuck on a plane or in a similar offline situation, like I am right now. It can also be much quicker than googling for a particular reference, as you can keep one terminal shell open with irb running all the time, and get your reference in an instant.

See what you can discover just by tinkering with help() or dir() commands in Ruby and Python.
