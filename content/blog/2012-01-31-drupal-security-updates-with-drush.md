---
title: Drupal Security Updates with Drush
date: 2012-01-31 00:00:00 Z
id: 465
author: Greg Boggs
guid: http://www.gregboggs.com/?p=465
url: "/drupal-security-updates-with-drush/"
categories:
- Blog
---

Since I get tired of hunting through forum threads for correct answers to common task. So, for the lucky souls to find this trick, here is how you run just the security updates to a Drupal install [with Drush][1] from the command line.

`drush upc -u 1 --pipe | grep 'SECURITY-UPDATE' | cut -d" " -f1 | xargs drush upc -u 1 -y`

Found [here][2].

 [1]: http://drupal.org/project/drush
 [2]: http://drupal.org/node/823146