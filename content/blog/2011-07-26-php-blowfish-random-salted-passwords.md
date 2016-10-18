---
id: 342
title: PHP Hash (bcrypt) Passwords with Random Salt
author: Greg Boggs

guid: http://www.gregboggs.com/?p=342
url: /php-blowfish-random-salted-passwords/
date: 2011-07-26
categories:
  - Blog
tags:
  - PHP
  - Security
menu: featured
---
We all know storing passwords in clear text in your database is rude. Yet, many do it because it makes a website easy for 
testing or password recovery. Programmers often don't hash passwords because we are lazy. But, I'm developing 
a WordPress security product. So, I should make an effort to securely hash passwords. It's just polite really. I know 
many of my users will set their password as Password1, but even so, I'd like to hash passwords. However, again I'm a 
lazy programmer, so I went to PHP.net to grab some code to steal for this. I thought I'd be done in 10 minutes.

It didn't take 10 minutes.

Instead I found the PHP man pages for storing passwords to be confusing, cryptic (haha get it?), and full of esoteric 
comments that are hard to understand. I don't really care about the minute differences between protocols, but I found
 that I[ shouldn't use md5][1]. I just wanted some sample code that works. I love the PHP manual, but when it comes to
  passwords the [man page][2] left me with more questions than answers. So, I read through everything on StackExchange, and 
  a [few][3] [good][4] [blogs][5]. I turned what I learned into some code so that you don't have to read them.

Here's the short version of what you need to know:

  1. Hash your passwords with something other than MD5 (Bcrypt or Sha2).
  2. Don't invent your own algorithm. You will fail.
  3. Use a unique, random salt for each password and store both the salt and hash.
  4. Salt does not have to be secret. Each salt has to be unique so the hashes are unique.
  5. Algorithms won't fix bad passwords.

Fork the [code on Github][6].

<script src="https://gist.github.com/Greg-Boggs/f9d4faa7429f5f89d689.js"></script>

 [1]: http://dev.mysql.com/doc/refman/5.5/en/encryption-functions.html
 [2]: http://php.net/manual/en/function.crypt.php
 [3]: http://www.richardlord.net/blog/php-password-security
 [4]: http://www.openwall.com/articles/PHP-Users-Passwords
 [5]: http://www.schneier.com/
 [6]: https://gist.github.com/Greg-Boggs/f9d4faa7429f5f89d689