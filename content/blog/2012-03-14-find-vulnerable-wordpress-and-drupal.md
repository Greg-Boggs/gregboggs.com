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

`grep 'DocumentRoot' /etc/httpd/vhost.d/* | awk {'print $2;'} | xargs -I {} nice find {} -name CHANGELOG.txt > ~/drupal-sites.txt`

## Produce clean report:

cat ~/drupal-sites.txt | xargs head -n 3 > ~/drupal-sites2.txt

## WordPress:

`grep 'DocumentRoot' /etc/httpd/vhost.d/* | awk {'print $2;'} | xargs -I {} nice find {} -name readme.html > ~/wp-sites.txt`

Todo: Add string to pull WordPress version with pretty formatting.

## Django:

     
    nice find -L /vol/www/ -name 'PKG-INFO' | xargs grep '^Version:' > ~/django-sites.txt