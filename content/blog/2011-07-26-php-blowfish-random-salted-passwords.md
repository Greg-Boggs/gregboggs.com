---
id: 342
title: PHP Hash (bcrypt) Passwords with Random Salt
author: greg
layout: post
guid: http://www.gregboggs.com/?p=342
url: /php-blowfish-random-salted-passwords/
date: 2011-07-26
categories:
  - Blog
tags:
  - PHP
  - Security
---
We all know storing passwords in clear text in your database is rude. Yet, many do it because it makes a website easy for testing or password recovery. Programmers often don&#8217;t hash passwords because we are lazy. But, I&#8217;m developing a WordPress security product. So, I should make an effort to securely hash passwords. It&#8217;s just polite really. I know many of my users will set their password as Password1, but even so, I&#8217;d like to hash passwords. However, again I&#8217;m a lazy programmer, so I went to PHP.net to grab some code to steal for this. I thought I&#8217;d be done in 10 minutes.

It didn&#8217;t take 10 minutes.

Instead I found the PHP man pages for storing passwords to be confusing, cryptic (haha get it?), and full of esoteric comments that are hard to understand. I don&#8217;t really care about the minute differences between protocols, but I found that I[ shouldn&#8217;t use md5][1]. I just wanted some sample code that works. I love the PHP manual, but when it comes to passwords the [man page][2] left me with more questions than answers. So, I read through everything on StackExchange, and a [few][3] [good][4] [blogs][5]. I turned what I learned into some code so that you don&#8217;t have to read them.

Here&#8217;s the short version of what you need to know:

  1. Hash your passwords with something other than MD5 (Bcrypt or Sha2).
  2. Don&#8217;t invent your own algorithm. You will fail.
  3. Use a unique, random salt for each password and store both the salt and hash.
  4. Salt does not have to be secret. Each salt has to be unique so the hashes are unique.
  5. Algorithms won&#8217;t fix bad passwords.

### Create a mySQL table to hold hashed passwords and random salt

> <pre><pre>--
-- SQL create script for for table `users`
--

CREATE TABLE IF NOT EXISTS `users` (
`user_id` mediumint(8) unsigned NOT NULL AUTO_INCREMENT,
`email` varchar(30) NOT NULL,
`reg_date` date NOT NULL,
`fname` varchar(20) DEFAULT NULL,
`lname` varchar(20) DEFAULT NULL,
`salt` char(21) NOT NULL,
`password` char(60) NOT NULL,
PRIMARY KEY (`user_id`),
UNIQUE KEY `email` (`email`)
) ;</pre></pre>

### PHP code required by both registration and validation

> <pre><pre>//ini_set("display_errors","1");
//ERROR_REPORTING(E_ALL);
CRYPT_BLOWFISH or die (&#039;No Blowfish found.&#039;);

$link = mysql_connect(&#039;localhost&#039;, &#039;wpscanner&#039;, &#039;aUvmxcxvTUPtW8Kw&#039;)
    or die(&#039;Not connected : &#039; . mysql_error());
mysql_select_db(&#039;wpscanner&#039;, $link)
    or die (&#039;Not selected : &#039; . mysql_error());

$password = mysql_real_escape_string($_GET[&#039;password&#039;]);
$email = mysql_real_escape_string($_GET[&#039;email&#039;]);

//This string tells crypt to use blowfish for 5 rounds.
$Blowfish_Pre = &#039;$2a$05$&#039;;
$Blowfish_End = &#039;$&#039;;</pre></pre>

### PHP code you need to register a user

> <pre><pre>// Blowfish accepts these characters for salts.
$Allowed_Chars =
&#039;ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789./&#039;;
$Chars_Len = 63;

// 18 would be secure as well.
$Salt_Length = 21;

$mysql_date = date( &#039;Y-m-d&#039; );
$salt = "";

for($i=0; $i&lt;$Salt_Length; $i++)
{
    $salt .= $Allowed_Chars[mt_rand(0,$Chars_Len)];
}
$bcrypt_salt = $Blowfish_Pre . $salt . $Blowfish_End;

$hashed_password = crypt($password, $bcrypt_salt);

$sql = &#039;INSERT INTO users (reg_date, email, salt, password) &#039; .
  "VALUES (&#039;$mysql_date&#039;, &#039;$email&#039;, &#039;$salt&#039;, &#039;$hashed_password&#039;)";
      
mysql_query($sql) or die( mysql_error() );

</pre></pre>

### Now to verify a user&#8217;s password

> <pre><pre>$sql = "SELECT salt, password FROM users WHERE email=&#039;$email&#039;";
$result = mysql_query($sql) or die( mysql_error() );
$row = mysql_fetch_assoc($result);

$hashed_pass = crypt($password, $Blowfish_Pre . $row[&#039;salt&#039;] . $Blowfish_End);

if ($hashed_pass == $row[&#039;password&#039;]) {
  echo &#039;Password verified!&#039;;
} else {
  echo &#039;There was a problem with your user name or password.&#039;;
}
</pre></pre>

 [1]: http://dev.mysql.com/doc/refman/5.5/en/encryption-functions.html
 [2]: http://php.net/manual/en/function.crypt.php
 [3]: http://www.richardlord.net/blog/php-password-security
 [4]: http://www.openwall.com/articles/PHP-Users-Passwords
 [5]: http://www.schneier.com/