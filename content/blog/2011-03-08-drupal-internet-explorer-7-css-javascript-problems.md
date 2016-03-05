---
id: 310
title: Drupal Internet Explorer 7 CSS Problems
author: Greg Boggs

guid: http://www.gregboggs.com/?p=310
url: /drupal-internet-explorer-7-css-javascript-problems/
date: 2011-03-08
categories:
  - Drupal
---
Internet Explorer is often the bane of a web designer's existence. Creating a design in Firefox or Chrome is easy, if something is off, click &#8220;inspect element&#8221; and you can fix the problem inminutes. However, in Internet Explorer, there's no such tool. Well, I had an issue with JQuery not displaying correctly on a Drupal site in IE7. It worked perfect in 8, Firefox, and Chrome. The demos for all the plugins I was using worked perfectly in Internet Explorer 7, but when I loaded them on the Drupal site, they were hosed. I checked the code over, and over, and over again. I have my [reservations about Drupal][1]. I hate how it creates so many external files, and how many &#8220;Gotchas&#8221; it has. I knew this had to be one of those weird Drupal quarks.

### Optimize CSS Files

After hours of frustration trying to get JavaScript to run, I opened the CSS file for IE in Drupal:

> * CSS targeted specifically for Internet Explorer for Windows.  
> *  
> * Any CSS in this file will apply to all versions of IE. You can target  
> * specific versions of IE by using conditional comments. See your sub-theme's  
> * .info file for an easy way to use them.  
> *  
> * While building your theme, you should be aware that IE limits Drupal to 31  
> * stylesheets total. The work-around for the bug is to enable CSS aggregation  
> * under: admin / settings / performance.  
> */

I turned CSS caching on and all my JQuery started working perfectly! I had overrun the limit for maximum allowed external files in IE7! How can Drupal possibly include more than 31 external files? Man, Drupal is insane. It's loading 2 files for every plugin I need. Anyway. Mystery solved. If you can't get JQuery, or CSS to work in Drupal on IE7, optimize your CSS files and see if that fixes all your problems.

 [1]: http://www.gregboggs.com/has-drupal-died/ "reservations about Drupal"