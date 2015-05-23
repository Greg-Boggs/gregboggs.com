---
id: 484
title: Find Vulnerable WordPress and Drupal
author: Greg Boggs

guid: http://www.gregboggs.com/?p=484
url: /find-vulnerable-wordpress-and-drupal/
date: 2012-03-14
categories:
  - Blog
---
## Drupal:

`grep &#039;DocumentRoot&#039; /etc/httpd/vhost.d/* | awk {&#039;print $2;&#039;} | xargs -I {} nice find {} -name CHANGELOG.txt > ~/drupal-sites.txt`

## Produce clean report:

cat ~/drupal-sites.txt | xargs head -n 3 > ~/drupal-sites2.txt

## WordPress:

`grep &#039;DocumentRoot&#039; /etc/httpd/vhost.d/* | awk {&#039;print $2;&#039;} | xargs -I {} nice find {} -name readme.html > ~/wp-sites.txt`

Todo: Add string to pull WordPress version with pretty formatting.

## Django:

     
    nice find -L /vol/www/ -name &#039;PKG-INFO&#039; | xargs grep &#039;^Version:&#039; > ~/django-sites.txt