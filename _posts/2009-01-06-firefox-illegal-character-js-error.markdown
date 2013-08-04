---
author: Ashish
comments: true
date: 2009-01-06 13:33:24+00:00
layout: post
slug: firefox-illegal-character-js-error
title: Firefox Illegal Character JS Error
wordpress_id: 48
tags:
- curl
- firebug
- javascript
- unicode
- utf8
---

I encountered the following error in FireBug (FireFox) on jQuery's ui.core.js that halts execution of the rest of my scripts:

`illegal character `

[caption id="attachment_80" align="alignnone" width="358" caption="Illegal Character error in Firebug"]![Illegal Character error in Firebug](http://ashish.tonse.com/wp-content/uploads/2009/01/illegal-character.png)[/caption]

The last time I encountered this problem, I renamed the file a few times and that fixed it. Yes, that makes no sense but as long as it was fixed, I just went about my merry self until it happened again today, and no amount of file renaming would fix it. So I did a little bit of investigation to figure out exactly why this happened.

<!-- more -->

First, I found this problem only happening in Firefox, and not Chrome, or IE.

When accessing the file directly in the browser, the first 3 chars were:

`﻿
/*
*
*
*
*
*/`

` `

`(function($) {
`

cURL returned the same result, narrowing it down to either the server adding that character, or the file containing it. Since the server is JBoss, it's most likely the file.

Opening the file in Binary mode in Textpad, I found that the first 3 bytes had the hex value: `EF BB BF`

This has to be a standard hex header for a certain file format (probably unicode related?) So I googled for that hex value. The first result was a [wikipedia entry](http://en.wikipedia.org/wiki/Byte-order_mark) for Byte-order mark. This made total sense already. The Byte-order mark specifies the byte order ([endianness](http://en.wikipedia.org/wiki/Endianness)) of the file that follows, with relation to unicode-related encodings. It turns out that `EF BB BF` is the Byte-order mark to denote UTF-8, but at the same time, it is completely unnecessary as UTF-8 has no byte-order issues by design.

So I had to get notepad++ to remove the first 3 bytes of that file, by choosing the option for "Encode in UTF-8 without BOM" in the Format Menu.

This fixed the issue! I hope this helps others that encounter this completely obscure looking error.
