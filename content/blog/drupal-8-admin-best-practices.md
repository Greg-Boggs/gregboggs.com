---
date: "2016-03-05T11:43:59-08:00"
title: "Drupal 8 Admin Best Practices"
author: Greg Boggs
url: /drupal-8-admin-best-practices/
categories:
  - Drupal
  - Best Practices
---
Drupal sites often suffer from a very poor editor experience. While Drupal 8 improves on the default experience by providing inline editting, working preview, and moving the 'advanced' options to the sidebar, there's still a lot of common mistakes that will lead to poor a experience. As a part of my on-going [Drupal 8 Best Practices](drupal8-site-building-best-practices/) series, lets look at what we can do to build good admin interfaces.

Here are a few major princiables behind the admin experience:

* Use permissions to hide unneeded options.
* Content should not be defined in code.
* Content and layouts should be editable by the editor without modifying code or css.
* Content should have a contextual edit link.
* A site should not require admin access to figure out how to edit.
* Content should be stored in nodes, not entities or taxonomy terms.
* Taxonomy can be used to apply additional page styles.
* Taxonomy terms should have limited fields.
* Vocabularies shouldn't be too large or too deep.
* The editor user should have links or a dashboard that links to key editor pages.
* Editors should be given the Clear Cache permission.
* CKeditor should be configured to allow pre-selected CSS styles.
* Editors should have a simple tool for applying layouts to new pages.
* Editors should be able to apply custom CSS via a drop down.

## Give Permissions Carefully

Clients should be given the admin password for user 1, but every user should log into the site with their own user account that has an 'editor' permission set. This editor account should only be given permission to do the things they do frequently. 

## Content Should be Editable

There's no reason to hard-code content into your theme or PHP. Every piece of text on the page should be editable through the hover edit link over that content. If you can't edit something without a git push, then it should be a blocking bug.

## Content Should be Stored in Nodes

This is a common mistake. Taxonomy terms are not content. They are meant to organize content. So, if you're putting fields (especially text fields) on terms, you're prboably making a pretty big error because taxonomy terms can't be unpublished, promoted, or revisioned easily. If you're putting content into custom entities, you're probably also making a mistake because entities take a lot of extra work to get the basics that you get from nodes for free.

## Give Editors Links and a Dashboard

Think of WordPress here, do you see your user profile when you first log in? No, you see a dashboard of content to edit and other useful information. Do the same in Drupal, redirect login to admin/content if nothing else. Give folks short cut links in their menu bar as well.

## Did You Clear the Cache?

Lets face it, the cache clear problem from Drupal 7 is a bit worse in Drupal 8. There are many times you need to Cache Rebuild. So, give them the button.

## Use a Layout System or Layout Taxonomy

Panels and Display Suite are popular because they are powerful, stable, uesful and easier to use than default Drupal. No matter what tools you use, give your editors easy abilitiy to apply a layout to a new page. Don't hand code each page. Build layouts, and apply them. Even a simple 'Layout' taxonomy field can allow editors to apply layouts to content. 

When deciding how to build things in Drupal 8, always spend some thought on how to make sure each piece of content will editted. Not only will your customers thank you, you'll be making Drupal look good.
