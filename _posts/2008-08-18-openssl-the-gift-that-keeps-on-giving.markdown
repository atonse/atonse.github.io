---
author: Ashish
comments: true
date: 2008-08-18 23:42:11+00:00
layout: post
slug: openssl-the-gift-that-keeps-on-giving
title: 'OpenSSL: The Gift that Keeps On Giving'
wordpress_id: 36
tags:
- linux
- security
- ssl
- unix
---

OpenSSL is just a gem of a package. It is so incredibly powerful, and does just about anything you could imagine that a crypto library could do. I am admittedly just an amateur at using this library, but when debugging an SSL issue where a cert was not verifying for me, I discovered this command through Tha Googles: 

    
    openssl s_client -connect www.logoworks.com:443 -showcerts


This shows you every step in which the SSL verification takes place, where the verification fails, etc. Really nifty.

<!-- more -->

But while you can get the MD5 hash of a file using the "md5" command (or "md5sum" on Linux), if you want to find the SHA1 or RIPEMD-160 hashes of a file, you can do so with:

    
    openssl sha1 whatever_filename
    openssl rmd160 whatever_filename


Also, from this [awesome tip](http://osxdaily.com/2007/05/02/quickly-encrypt-a-file-with-openssl/) from OS X Daily, you can quickly encrypt a file using openssl using the following (I used AES 128 in CBC mode) -- it even prompts you for the encryption password (key) twice:

    
    openssl aes-128-cbc -e -in filetoencrypt.txt -out encryptedfilename


and decrypt with:

    
    openssl aes-128-cbc -d -in encryptedfilename -out decryptedfilename


It prompts you for the decryption password once and you're all set.

I'm still discovering all the goodies inside the OpenSSL command. But so far, it's proving to be incredibly powerful awesome. I understand it's the underlying library for SSH, one of the workhorse protocols of the secure internet, but I didn't know that so much functionality was exposed through the console.

Update: Wow Ok misconception. I thought OpenSSH was based on OpenSSL - it's not. It's apparently a common misconception. :)
