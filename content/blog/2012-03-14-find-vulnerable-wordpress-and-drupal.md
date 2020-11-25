---
title: Find Vulnerable WordPress and Drupal
date: 2012-03-14
id: 484
author: Greg Boggs
guid: http://www.gregboggs.com/?p=484
url: "/find-vulnerable-wordpress-and-drupal/"
categories:
- Drupal
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
