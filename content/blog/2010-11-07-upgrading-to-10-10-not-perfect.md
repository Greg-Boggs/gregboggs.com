---
id: 260
title: 'Upgrading to 10.10 wasn&#8217;t a perfect 10.'
author: greg
layout: post
guid: http://www.gregboggs.com/?p=260
url: /upgrading-to-10-10-not-perfect/
date: 2010-11-07
categories:
  - Blog
tags:
  - Ubuntu
---
<a rel="attachment wp-att-264" href="http://www.gregboggs.com/upgrading-to-10-10-not-perfect/startupgrade/"><img class="alignleft size-medium wp-image-264" title="startupgrade" src="http://www.gregboggs.com/wp-content/uploads/2010/11/startupgrade-400x355.png" alt="" width="400" height="355" /></a>Upgrading Ubuntu has always been difficult. I put myself through the updater before doing a fresh install hoping I can either fix the problems or, at least, experience them before giving up and using a fresh install. One of my favorite [Canonical bloggers][1] asked [why do people insist][2] on fresh installs. Hopefully this post sheds some light on why upgrades still hurt.

Most of my problems stem from the fact that I install programs on my system and change a few minor settings here and there. But, who doesn&#8217;t install software on their computer?

All told, the upgrade took roughly 6 hours. Much of that time was spent with my laptop doing nothing while waiting for me to click forward, close, upgrade, or reboot. Here&#8217;s a short list of bugs that came up in my first 5 minutes of using Maverick:

1. Firefox didn&#8217;t work! Yes, it&#8217;s a documented bug. Two of my plugins caused it to fail. Quake Live and libmoon. The fixes:

  * cd ~/.mozilla/firefox/ii3ird8a.default/extensions; rm -rf quake<tab>
  * sudo apt-get remove libmoon

2. I got asked for my root password after logging in even though I have my desktop set to auto login. That&#8217;s going to be tricky to track down. I&#8217;ve always had to type my password to connect to my wireless&#8230; which sucks. I was hoping that would be fixed. Maybe next release.

3. Enhanced visual affects still has annoying interface bugs. Scrolling near my clock (or any top right interface button) causes the desktop switcher to come on. HIGHLY annoying. Also, the &#8220;show desktop&#8221; button doesn&#8217;t function as expected. Both are easy to fix by disabling enhanced visual affects, but I miss my wobbly windows! Oh well. maybe 11.04 will fix it.

4. I still don&#8217;t have a volume control applet. This is a lingering bug from the last upgrade that I haven&#8217;t fixed yet. In the meantime, I use my laptop function keys to adjust my volume. Highly annoying considering I use an external full size keyboard.

5. My desktop appears exactly as it did in 10.04. And, I had no option to use the new design during the upgrade. Although, I am loving the new font. And, I&#8217;m sure this will be a quick fix.

Update:  
6. Clicking links in thunderbird or pidgin don&#8217;t open a web browser.

7. Flash doesn&#8217;t work anymore. It says &#8220;missing plugin&#8221; then when I go to install Flash, FF says it&#8217;s already installed.

8. Sound still doesn&#8217;t work on the system when JVM is running, left over bug from 10.04&#8230; can fix it by running my jvm program with aoss, but then the JVM is unstable and my Java program goes crashy crashy. I&#8217;ve also noticed system freezes (100% cpu usage) while running Java programs that didn&#8217;t happen in 10.04

The updater itself was clunky and bothered me with confusing questions while refusing to move forward without constant babysitting. This is nothing new to Ubuntu. The interface works exactly like the apt-get technology behind it. A common problem in interface design. I do hope the next version of Ubuntu streamlines the updater. I&#8217;d love to click update answer a few easy questions, and come back a few hours later to a completely updated computer. If you have any hints on fixing my update quirks, drop a comment.

 [1]: http://castrojo.tumblr.com
 [2]: http://castrojo.tumblr.com/post/1093664654/no-need-to-complicate-your-life