---
title: Zappos shares your password with hackers
date: 2012-01-19
id: 444
author: Greg Boggs
guid: http://www.gregboggs.com/?p=444
url: "/zappos-shares-your-password-with-hackers/"
categories:
- Blog
---

<img class="alignleft" title="Zappos" src="http://blogs.zappos.com/assets/hotspot/timeslot_images/10425_1311613627.png" alt="Zappos logo" width="157" height="86" />So, while I've been slaving away trying to get my own blog to pass my [WordPress security scanner][1], Zappos got hacked. It happens. They were probably running WordPress right? Their customer information was accessed. While they didn't make an announcement, [they did email their customers][2] and tweet about it. While I'm happy with their proactive response, this provides a wonderful learning opportunity for all of us who store passwords for a living. When a user gives you a password, they trust that you will keep it safe, and that you won't share it with anyone. Part of keeping passwords safe is storing them well.

Now, Zappos comment on the hack:

> We are writing to let you know that there may have been illegal and unauthorized access to some of your customer account information on Zappos.com, including one or more of the following: your name, e-mail address, billing and shipping addresses, phone number, the last four digits of your credit card number (the standard information you find on receipts), and/or your **cryptographically scrambled** password (but not your actual password).

<http://blogs.zappos.com/securityemail> (emphasis mine)

They further add, &#8220;We also recommend that you change your password on any other web site where you use the same or a similar password.&#8221; 99% of their customers are going to ignore the email even if it gets through their spam filter. So, my question for Zappos tech team is,

## How did you store the passwords?

MY guess is that they used an MD5 which is NOT cryptographically scrambling a password, and it is **not secure **password storage. But, it's what everyone does. If you store user passwords with Md5 hash still, or worse, in plaintext like my student loan servicing company, MD5 has been broken for years. You should always store your user's passwords with a secure method like using [bcrypt with random salt][3]. That way, when someone copies your database, your user accounts are still secure.

 [1]: http://www.scanwp.com "WordPress Security Scanner"
 [2]: http://goodexperience.com/2012/01/zappos-doesnt-mention.php
 [3]: http://www.gregboggs.com/php-blowfish-random-salted-passwords/ "PHP Hash (bcrypt) Passwords with Random Salt"
