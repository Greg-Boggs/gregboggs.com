---
id: 187
title: How Would You Configure High Traffic Webservers?
author: Greg Boggs

guid: http://www.gregboggs.com/?p=187
url: /how-would-you-configure-high-traffic-webservers/
date: 2010-10-13
categories:
  - Blog
tags:
  - Apache
  - mySQL
  - System Administration
---
<a rel="attachment wp-att-200" href="http://www.gregboggs.com/how-would-you-configure-high-traffic-webservers/traffic/"><img class="alignleft size-full wp-image-200" title="traffic" src="http://www.gregboggs.com/wp-content/uploads/2010/10/traffic.jpg" alt="" width="148" height="240" /></a>Today I was asked the question, &#8220;Should I separate the Apache server from mySQL server?&#8221; This brings up a great question. What&#8217;s the best way to configure a small set of servers for multiple high-traffic websites? Once you outgrow a single dedicated server, where do you go? Do you buy a big expensive dedicated server? What happens when that one is maxed out, do you buy two?

If you buy two servers, do you split Apache and mySQL? Do you use a load balancer even though it costs as much as a third server? Do you set up an [Apache cluster with heartbeat][1]? I find lots of tutorials on how to set up complex configurations, but so far I&#8217;ve found very little on which configurations you should use and why.Do you cloud? Do you set up virtualization on your own dedicated server? If so which software do you choose?

Hosting companies are no help. They just want to sell you a machine and be done with it. My inner nerd circle has lots of ideas, but none of us really know what the best way is. The main variables I see in this problem are as follows:

  1. Response Time
  2. Fault Tolerance
  3. Configuration Difficulty
  4. Cost

So, how do you maximize response time and fault tolerance without maximizing difficulty and cost? Got a link with the answer? Or, just care to throw in 2 cents? Drop a comment.

 [1]: http://www.howtoforge.com/high_availability_heartbeat_centos