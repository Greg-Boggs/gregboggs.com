---
id: 173
title: 'WordPress Images Won&#8217;t Align'
author: greg
layout: post
guid: http://www.gregboggs.com/?p=173
permalink: /wordpress-images-wont-align/
date: 2010-10-07
categories:
  - Blog
tags:
  - WordPress
---
WordPress relies on themes to allow users to align images and create captions. If your theme doesn&#8217;t support alignment or captions, you&#8217;ll find adding images to WordPress to be very frustrating.

WordPress[ provides documentation][1] to fix this problem, but it&#8217;s requires that you edit your theme&#8217;s CSS file:

> .aligncenter, div.aligncenter {  
> display: block;  
> margin-left: auto;  
> margin-right: auto;  
> }  
> .alignleft {  
> float: left;  
> }  
> .alignright {  
> float: right;  
> } 

### Backup your Theme First

Before you edit your WordPress theme, always make sure you have a backup because WordPress editor does not allow you to undo mistakes.

 [1]: http://codex.wordpress.org/CSS