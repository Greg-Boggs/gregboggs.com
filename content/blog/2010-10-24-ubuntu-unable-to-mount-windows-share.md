---
id: 236
title: Ubuntu unable to mount windows share
author: Greg Boggs

guid: http://www.gregboggs.com/?p=236
url: /ubuntu-unable-to-mount-windows-share/
date: 2010-10-24
categories:
  - Blog
tags:
  - Ubuntu
---
I haven't been able to get my Ubuntu laptop on Windows network for years. This is the best walk through I've found. Unfortunately, my apt-get is broken&#8230; so I couldn't do apt-get install win-bind. But, one of the other steps solved the problem.

smbtree returns:  
cli\_start\_connection: failed to connect to JANES<20> (0.0.0.0). Error NT\_STATUS\_UNSUCCESSFUL

Walk through that hasn't resolved the problem yet:

http://ubuntuforums.org/showthread.php?t=1169149

sudo /etc/init.d/networking restart does not work in Ubuntu 10.04! However, following the walk through and rebooting completely did work! I can browse networks again!