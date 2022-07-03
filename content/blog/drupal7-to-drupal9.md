+++
author = "Kana Patrick"
categories = ["Drupal"]
date = "2022-07-03"
draft = false
tags = ["Drupal"]
title = "Migrating a website from Drupal 7 to Drupal 9"
url = "/upgrade-drupal7-to-drupal9-migration/"
+++

This is a guest post by [Kana Patrick](https://kanapatrick.cm/en/get-quote) who is a world-class Drupal migration expert.

The end of life of Drupal 7 is getting closer and every day more and more website owners are starting the migration. This process is not easy and almost always takes a long time. I recently migrated a client's site from Drupal 7 to Drupal 9. The purpose of this article is to share with you my modest experience.

## Different migration processes from drupal 7 to Drupal 9

There are essentially 2 ways to migrate a site from Drupal 7 to Drupal 9:

- Updated the site using the migration scripts provided by the Drupal core (Based, since Drupal 8, on the Migrate community module and now in the core);
- Create a completely new Drupal 9 site, and attempt to recover the contents of Drupal 7 (again using Migrate-based tools).

In general, I recommend the second solution, as it is the one that was used in the case of the migration of the Northwest Analytics Inc. Site and it is the one that often generates the least constraints by promising a transformation of the content as needed.

The website on drupal 7 was launched in 2011 and before the migration
started, it had :
- 5K+ Users
- 3K+ Medias
- 12k+ Noeuds
- 20K+ Webform submission

Note that the site had multilingual content

Can you imagine those crazy numbers?

But despite this size, generally, the whole migration consists of 4 main steps:

1. Creation of mappings from the old Drupal 7 site to the new Drupal 9 site.
2. Creation of the appropriate entities/fields on the Drupal 9 site.
3. Content migration itself by migrating module from Drupal 9 core.
4. Both Contrib and Custom functionality implementation/migration.
5. Theme migration.
6. Production deployments and content managers studying.

Of course, it sounds easier than it is. I have faced many complex and interesting challenges during my migrations. I will do another article on it so I can share my difficulties with you.

As time goes by, the migration becomes more and more expensive and the old Drupal 7 site is more and more challenging to maintain. Take courage and start migrating your Drupal 7 project to Drupal 9 today. Looking to migrate from your current Drupal 7 site to the new Drupal 9? I invite you to [contact me](https://kanapatrick.cm/en/get-quote) for your Drupal site migration projects!
