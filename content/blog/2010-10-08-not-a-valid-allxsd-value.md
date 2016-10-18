---
title: Not a valid AllXsd value
date: 2010-10-08 00:00:00 Z
id: 180
author: Greg Boggs
guid: http://www.gregboggs.com/?p=180
url: "/not-a-valid-allxsd-value/"
categories:
- Blog
tags:
- PHP
- Web Services
---

Today I was programming a PHP client that uses an XML-RPC web service. One of the fields the service requires is a date/time field as an AllXsd value. When you give the field a date in any other format it returns the error: Not a valid AllXsd value. What the heck is that?? How did anyone program before search engines and the Internet?

The format it requires is:

> yyyymmddThh:mm:ss  
> 20100209T11:30:32

To generate a valid AllXsd value for a date time using PHP is extremely easy:

> date(c);