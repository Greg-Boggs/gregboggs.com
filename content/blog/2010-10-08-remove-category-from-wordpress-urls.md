---
id: 184
title: Remove category from WordPress URLs
author: Greg Boggs

guid: http://www.gregboggs.com/?p=184
url: /remove-category-from-wordpress-urls/
date: 2010-10-08
categories:
  - Blog
tags:
  - WordPress
---
The theme I use for this website creates a blog by using a separate category in WordPress for blog posts. Normally I prefer to use static pages for non-blog pages, and rely on posts for the blogging feature. This method is easy to set up and creates an easy to manage, less confusing installation. However, category-based blogging came built into the theme, and tearing it out would be a lot of wasted effort.

Instead I removed the &#8220;category&#8221; word from my URLs because &#8220;category&#8221; adds no meaning. My blog was found at www.gregboggs.com/category/blog&#8230; try sharing that URL over the phone. Now, my blog is gregboggs.com/blog/ which is much easier.

To accomplish this feat I had to:

  1. install a plugin called redirection
  2. set category as my source URL
  3. leave my destination URL blank
  4. install a plugin called decategorizer

I still have to remember to categorize all my blog posts in the blog category, but I no longer have to remember to type /category/blog when sending someone my blog&#8217;s address. I can also safely switch themes and not have to worry that my blog posts will move.