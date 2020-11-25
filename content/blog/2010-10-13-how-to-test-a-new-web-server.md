---
title: How to Test a New Web Server?
date: 2010-10-13
id: 192
author: Greg Boggs
guid: http://www.gregboggs.com/?p=192
url: "/how-to-test-a-new-web-server/"
categories:
- Blog
tags:
- Apache
- DNS
- Web Design
---

> I'm moving to a new web host. Apache, mySQL, Drupal, etc&#8230; Virtual web sites. How do I test virtual web sites before changing the DNS? For example, there is a virtual site [http://www.example.com][1], but [http://www.example.com][1] is still pointing to the old server. How do I test it on the new server?

Apache will respond to a visitor according to it's Virtual Host file. So, when you visit a server by it's IP address(123.123.123.123) , you won't see your website. You must use your domain name so that Apache can retrieve the correct files for your website. To test a new Apache server before moving a live website you can edit the local domain name files on your personal computer to point your domain to the new website.

On Ubuntu:  
Edit the file /etc/hosts to read www.example.com 123.123.123.123

On Windows the file is in system32&#8230; or some such place. It's different for every version of Windows.

Now when you visit www.example.com you'll go to the new server while the entire rest of the world still sees the old server. You can now test the new website while the old website is still on the Internet. The best part is, you don't have to use a funky address like test.example.com and then change the URL. The only file you have to update once the website is live is the hosts file on your own computer.

 [1]: #
