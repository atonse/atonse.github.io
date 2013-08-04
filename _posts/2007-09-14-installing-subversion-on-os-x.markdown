---
author: Ashish
comments: true
date: 2007-09-14 04:32:34+00:00
layout: post
slug: installing-subversion-on-os-x
title: Installing Subversion on OS X
wordpress_id: 11
tags:
- apple
- leopard
- osx
- subversion
---

I would think that building and installing Subversion on OS X from source would be slightly more straightforward than it was. But it might start to confuse some of the less comfortable, so I thought I'd write up this step-by-step guide.

We'll be creating a lot of compilation and linking across directories, so it's good to keep it all contained in one place. So let's start by creating a directory in the user's home that's going to contain all this.

`mkdir ~/svncompile
cd ~/svncompile`

Before you really get started, download the following files and extract them:

Subversion (all releases latest as of Sep 13, 2007)

`curl -O http://subversion.tigris.org/downloads/subversion-1.4.5.tar.bz2
tar jxf subversion-1.4.5.tar.bz2`

Apache Portable Runtime (apr):

`curl -O http://www.mirrorgeek.com/apache.org/apr/apr-0.9.16.tar.gz
tar zxf apr-0.9.16.tar.gz`

Apache Portable Runtime Utilities (apr-util):

`curl -O http://www.mirrorgeek.com/apache.org/apr/apr-util-0.9.15.tar.gz
tar zxf apr-util-0.9.15.tar.gz`

If you do an ls, you should have the following directories extracted:

`drwxr-xr-x   44 ashish  ashish     1496 Sep  3 21:43 apr-0.9.16
drwxr-xr-x   34 ashish  ashish     1156 Sep  3 21:46 apr-util-0.9.15
drwxr-xr-x   29 ashish  ashish      986 Aug 14 06:18 subversion-1.4.5`

Next, we're going to compile the dependency libraries, apr and apr-util. We configure, then make, and finally make install:

`cd apr-0.9.16
./configure
make
sudo make install
cd ..`

apr-util depends on apr, so when we configure apr-util, we need to point it to apr:

`cd apr-util-0.9.15
./configure --with-apr=../apr-0.9.16
make
sudo make install
cd ..`

Using --with-apr tells the utils to use that instance of apr located in the directory we just built.

Building SVN

And finally, we can build svn. :-)

First, we go to svn and run configure, but we point it to apr and apr-utils:

`cd subversion-1.4.5
./configure --with-apr=../apr-0.9.16 --with-apr-util=../apr-util-0.9.15`

Subversion might tell you that you don't have BerkeleyDB installed. I'll have to modify this section for that.

Now build and install subversion:

`make
sudo make install`

And that's it! Assuming all went well, you should be able to type "svn" and get an svn usage message.

Cleanup

There are two cleanup options, depending on what you want to do. If you just want to get rid of all of the source, the easy thing to do is:

`rm -rf ~/svncompile`

And we're done. If you want to hold on to the source, I always prefer keeping the source directory clean because that saves space if you're not actively developing and also keeps your directories, well, clean.  For that, just run make clean on each of those projects:

`cd apr-0.9.16
make clean
cd ../apr-util-0.9.15
make clean
cd ../subversion-1.4.5
make clean`

And you have a clean source repo. :-)

To put it all together, here are all the commands you need to fully install Subversion 1.4.5 on Mac OS X 10.4 (Tiger):

`mkdir ~/svncompile
cd ~/svncompile
curl -O http://subversion.tigris.org/downloads/subversion-1.4.5.tar.bz2
tar jxf subversion-1.4.5.tar.bz2
curl -O http://www.mirrorgeek.com/apache.org/apr/apr-0.9.16.tar.gz
tar zxf apr-0.9.16.tar.gz
curl -O http://www.mirrorgeek.com/apache.org/apr/apr-util-0.9.15.tar.gz
tar zxf apr-util-0.9.15.tar.gz
cd apr-0.9.16
./configure
make
sudo make install
cd ..
cd apr-util-0.9.15
./configure --with-apr=../apr-0.9.16
make
sudo make install
cd ..
cd subversion-1.4.5
./configure --with-apr=../apr-0.9.16 --with-apr-util=../apr-util-0.9.15
make
sudo make install`

Hope this helps!! Leave me a comment if you have any problems following the guide.
TODO: mod_dav_svn and BerkeleyDB support.
