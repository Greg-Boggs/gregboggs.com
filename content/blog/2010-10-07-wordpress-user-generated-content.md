---
title: WordPress User Generated Content
date: 2010-10-07 00:00:00 Z
id: 151
author: Greg Boggs
guid: http://www.gregboggs.com/?p=151
url: "/wordpress-user-generated-content/"
theme: right-sidebar
categories:
- Blog
tags:
- Free Software
- WordPress
---

An amazing start-up that I provide consulting for recently used WordPress to build user-generated [consumer complaints][1] feature. The idea behind ConsumerBell is to empower consumers by grouping their complaints together and giving them leverage. For ConsumerBell to work, they need complaints! So, they built a beautiful feature for users to submit and publish their complaints.

There are several ways to publish moderated user-generated content in WordPress. ConsumerBell built a custom plugin, but I've found some other interesting ways to solve the problem of generating user created content **without programming**. For example, WordPress includes comments which can be used to create simple content. However, comments have many drawbacks because a comment doesn't create a new post inside WordPress. So, all your user content is confined to a single page of your site. After some digging I've turned up several other methods to generate moderated content.

The three methods I found were using:

  1. Built-in e-mail posting and a contact form
  2. TDO Mini Forms
  3. Gravity Forms

### E-Mail Posting and a Contact Form

The most [innovative solution][2] to the problem is to use built in post by e-mail and a simple contact form. The basic idea is to set up any [WordPress contact form][3], and configure it to send &#8220;contact&#8221; emails directly to WordPress' built in post by e-mail functions. Once the two features are set up, a little work on your theme, and you're capturing product reviews, customer complaints, or user generated blog posts. When you configure [post by email][4], you should make sure to use an email address that does not match a registered users email. This will ensure that all new user generated content is not published automatically. It will be posted &#8220;pending review&#8221;. Lastly, if you need images in the content, check out [Postie][5].

### TDO Mini Forms

The second solution is to use the popular [TDO Mini Forms][6] plug in which is designed to create user generated posts in WordPress. The plug in looks very powerful, but the administration screens seemed fairly complex. If you need fine grained control over your user generated content, give this plug in a try.

### Gravity Forms

The last solution is Gravity Forms. These people give the appearance that their plug in can only be obtained by purchasing it from them. However, all WordPress is protected by the GPL making all WP plugins [Free software][7]. So, Gravity Forms is Free software too. If anyone has a copy of Gravity Forms, [please share][8] it. What you do get by paying for Gravity Forms is support.

### My Solution

When I need user-created content in WordPress, I'll probably rely on a simple contact form because it requires no programming and I found TDO Mini Forms too complex.

 [1]: http://www.consumerbell.com
 [2]: http://millionclues.com/guest-posts/use-wordpress-to-create-user-generated-content-site/
 [3]: http://contactform7.com/
 [4]: http://codex.wordpress.org/Post_to_your_blog_using_email
 [5]: http://robfelty.com/plugins/postie
 [6]: http://thedeadone.net/download/tdo-mini-forms-wordpress-plugin/
 [7]: http://www.gnu.org/philosophy/free-sw.html
 [8]: contact