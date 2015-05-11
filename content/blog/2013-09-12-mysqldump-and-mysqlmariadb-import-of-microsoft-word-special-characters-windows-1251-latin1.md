---
id: 724
title: Mysqldump and mySQL/Mariadb import of Microsoft Word Special Characters Windows 1251 (Latin1)
author: greg
layout: post
guid: http://www.gregboggs.com/?p=724
permalink: /mysqldump-and-mysqlmariadb-import-of-microsoft-word-special-characters-windows-1251-latin1/
date: 2013-09-12
categories:
  - Blog
---
I needed to export and import a WordPress database from Dreamhost. So, I logged in via command line dumped the files with:

    
    mysqldump -u user -p > databases.sql
    

I then copied those files to the new server and ran  


    
    mysql -u user -p < databases.sql
    

Everything was going great until I loaded a blog post with Microsoft Word special quote marks in it. Arrg! I managed to get the files with quotes intact out of dreamhost with this:

    
    mysqldump --default-character-set=latin1 -u user -h host.example.com -p > databases.sql
    

However, In Mariadb on the new server Microsoft special characters were still wrong on the new server after the import!

So I ran this:

    
    UPDATE wp_posts SET post_content =
        IFNULL(CONVERT(CONVERT(CONVERT(post_content USING latin1)
                                           USING binary)
                                           USING utf8),
                                        post_content )
    

Life is good. MariaDB now correctly displays WordPress posts with all the Microsoft Windows 1251 &#8211; Latin1 junk.