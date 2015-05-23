---
id: 249
title: Running PHP via Cron
author: Greg Boggs

guid: http://www.gregboggs.com/?p=249
url: /running-php-via-cron/
date: 2010-10-29
categories:
  - Blog
tags:
  - cron
  - PHP
---
Three very annoying things I never, ever want to forget (again) about running PHP via the command line using cron:

  1. Cron has strange paths so, include (&#8216;./common.php&#8217;); will not work! You have to use (&#8216;common.php&#8217;);
  2. If you have blank lines in your output file, check for blank lines before and after your PHP tags
  3. Remember to specify the full path to your script

Tip: Remember to redirect error output 2>1& when using php via cron, and also don&#8217;t forget to append to your log file with >> operator.

Cron my php script to run every 5 minutes:

\*/5 \* \* \* * php /var/www/sites/getfaxstatus.php >> /var/www/sites/output.php 2>1