---
author: admin
comments: true
date: 2009-06-15 16:00:31+00:00
layout: post
slug: netstat-is-your-friend
title: Netstat is your friend
wordpress_id: 134
---

Every now and then, you need to run a server like JBoss, whose services bind to a handful of default ports (1099, 1098, 8080). And occasionally, you get a JVM_Bind error for these ports:

    
    java.net.BindException: Address already in use: JVM_Bind 
    Cause: java.rmi.server.ExportException: Port already in use: 1098;


The first (and more obvious) solution is to check that there isn't already an instance of JBoss. Once you've made sure (by killing all java.exe/javaw.exe processes), how do you find out what program is still listening on a particular port?

Netstat will help you there.

<!-- more -->**Netstat**

Netstat (or equivalent) is a utility available in all major OSs, and allows you to view protocol statistics.  You can view incoming and outgoing ports that are in use, along with the IPs and hostnames that the sockets are connected to. In Windows, typing **netstat -ab** (-a for all connections, -b for the executable involved) in the command prompt results in a list of TCP and UDP sockets and the name of the process that is listening on that socket. Here's some example output:

    
      TCP    MyComputerName:6060    MyComputerName:0       LISTENING       1132
      [ibmtcsd.exe]
    
      TCP    MyComputerName:1026    MyComputerName:0       LISTENING       1508
      [UNS.exe]
    
      TCP    MyComputerName:1141    MyComputerName:0       LISTENING       28668
      [googletalkplugin.exe]
    
      TCP    MyComputerName:5152    MyComputerName:0       LISTENING       1572
      [jqs.exe]
    
      TCP    MyComputerName:5354    MyComputerName:0       LISTENING       896
      [mDNSResponder.exe]
    
      TCP    MyComputerName:27015   MyComputerName:0       LISTENING       12500
      [AppleMobileDeviceService.exe]
    
      TCP    MyComputerName:netbios-ssn  MyComputerName:0       LISTENING       4
      [System]
    
      TCP    MyComputerName:1141    localhost:1142         ESTABLISHED     28668
      [googletalkplugin.exe]
    
      TCP    MyComputerName:1142    localhost:1141         ESTABLISHED     29716
      [chrome.exe]
    
      TCP    MyComputerName:1405    localhost:1406         ESTABLISHED     33508
      [firefox.exe]


Hope this helps you track down that annoying process that's keeping JBoss from loading.
