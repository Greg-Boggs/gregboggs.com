---
title: Drupal 8 Breadcrumbs - Add the Current Page
date: 2016-03-04 19:36:49 Z
author: Greg Boggs
url: "/drupal8-breadcrumbs/"
categories:
- Drupal
- Best Practices
tags:
- Drupal Config
menu: featured
---

Breadcrumbs are a pain point in Drupal 7. If you don't know how breadcrumbs are supposed to work, [go read this](https://www.nngroup.com/articles/breadcrumb-navigation-useful/). The crumb should start with home and continue through to an unlinked crumb of the current page. Crumbs were implemented poorly, and breadcrumbs were difficult to modify in a module. Further, they were based on items in the menu. The breadcrumbs didn't even allow you to edit the home title or include the current page title as an unlinked crumb. So, if you wanted breadcrumbs on a Drupal site, the first step was to choose 1 of 10 different modules to build them for you. Making matters worse, some themes decided to program breadcrumbs for you as well. If you're stuck with a Drupal 7 breadcrumb problem, use a module I help maintain, [Easy Breadcrumb](https://www.drupal.org/project/easy_breadcrumb). Trust me. I've got this for you.

## Breadcrumb Improvements

 Drupal 8 vastly improves breadcrumbs, but core still gets them wrong. They are based on the current page path exactly like Easy Breadcrumb in Drupal 7 which is a huge improvement. So, what did they get wrong? The current page title is missing. Bummer. So close. But, not hard to fix. So, lets do it! If someone tells you to program the breadcrumbs into your theme, don't listen to them. They are doing it wrong. Themes should work with markup and presentation. They shouldn't implement complex, reusable logic. 
 
 Drupal 8 has refactored breadcrumbs [making them much easier](https://www.palantir.net/blog/d8ftw-breadcrumbs-work) for developers to extend or replace. This new architecture makes it easy for us to correct Drupal 8's breadcrumbs. Unfortunately, the code from Larry's post is a bit out of date and doesn't work anymore. So, lets look at the code pulled from my module Current Page Crumb module that [adds the current page title](https://www.drupal.org/sandbox/gregboggs/2664958) to the breadcrumb.
 
 <script src="https://gist.github.com/Greg-Boggs/2338e65e6e60b8812ed7.js"></script>
 
 This code extends the PathBasedBreadcrumbBuilder core class to add the current page title to the breadcrumb. Since everything else needed for the breadcrumb is handled by the parent, line 31 does almost all the work for us. From there, we just need a few lines to add the current page's title. If you're looking for more examples to completely replace the core breadcrumbs with a custom builder, check out the [Drupal 8 version of Easy Breadcrumb](https://github.com/Greg-Boggs/easy_breadcrumb) which does just that.