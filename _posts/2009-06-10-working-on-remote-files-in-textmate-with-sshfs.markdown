---
author: admin
comments: true
date: 2009-06-10 01:30:34+00:00
layout: post
slug: working-on-remote-files-in-textmate-with-sshfs
title: Working on Remote Files in TextMate with SSHFS
wordpress_id: 122
---

I've been developing Wordpress templates for a client lately and it helps to have the templates directly on the server so I can work easily with the designer and she can see all my updates immediately. So this is what I want to be able to do:



	
  * Edit files on the server in a secure way

	
  * Use Textmate or a local editor

	
  * Not have to run rsync or any sync/upload utility


Enter MacFUSE (and MacFusion) and SSHFS.

<!-- more -->[MacFUSE](http://code.google.com/p/macfuse/) is an OS X port of the excellent [FUSE](http://fuse.sourceforge.net/) (Filesystem in User Space) project. It allows you to build your own "filesystem" quite easily. (technical [video](http://www.youtube.com/watch?v=cY8lBOSO3ak) on MacFuse available) Some nifty filesystems include:



	
  * SSHFS - allows you to mount a directory on a remote server over SSH, as a local Volume

	
  * FTPFS - same, but using FTP


The beauty of this is, programs that are only designed to edit local files can now edit remote files without realizing it.


### Step 1: Mount the remote folder as a local volume


First, [download MacFusion](http://www.macfusionapp.org/), which allows you to setup your SSH server parameters and mount it as a local volume. I was initially going to type out sshfs shell commands, but this is a much cleaner solution.

MacFusion should be intuitive enough that you can enter the host, username, password, and main directory. For extra security (yes, this actually is more secure), use public key authentication for SSH with the added convenience of auto-login (if your certificate doesn't have a password).


### Step 2: Edit in Textmate (or other editor)


Textmate (TM) is slow while using SSHFS for various reasons.

Firstly, when TM loses focus (say, you activate your browser) and regains focus, it rescans your project directory for any file changes. While this is a nifty and near-instantaneous feature for a local volume, it will take a few seconds on a remote server. There's a quick remedy for that: [ReMate](http://ciaranwal.sh/remate/) - a TM plugin that disables the project folder refresh. This will make the experience much more bearable.

Saving files will result in a noticeable lag, but I think this is overall a good solution for having your cake files on a remote server) and eating it too.

Anyone inclined to suggest source control or rails like capistrano deployment scripts, this is a quick and dirty solution for wordpress themes and editing files on the server for instant feedback. For more complex apps, those deployment packages will do a much better job.
