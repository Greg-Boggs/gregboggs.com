---
date: "2016-02-18T11:43:59-08:00"
title: "Drupal 8 Configuration Workflow Best Practices"
author: Greg Boggs
url: /drupal-configuration-best-practices/
categories:
  - Drupal
  - Best Practices
---
Don't store site configuration in the database during development because putting configuration in the database makes configuration difficult to track in version control. Instead, [use the file system](https://www.drupal.org/node/2416555)! Putting configuration in a database also makes it more difficult to restore, compare, sync, deploy, modify, and review the site config. Drupal 8 uses Yml files for configuration which are a perfect format for file-based configuration. In fact, this is the only method for [storing configuration in BackdropCMS](http://www.jenlampton.com/blog/managing-backdrop-cms-config-files-git) because BackdropCMS uses JSON files to store site configuration. Drupal uses Yaml to store your configuration the database, but storing Yaml in files was the default method for Drupal 8 when CMI was released. Many posts have been written about the [default workflow](http://nuvole.org/blog/2014/aug/20/git-workflow-managing-drupal-8-configuration) for configuration. But, the promise of file-based workflow is more efficient.

## Configuring in Files Workflow

When Drupal stores configuration files in the file system, all you do to save your work is run a git commit because as soon as you click save in a form, Drupal writes your changes to the configuration folder. Once your work is in code and committed to version control, you can publish those on GitHub and open a pull request to review your work before deploying it to production. This workflow is possible with database configuration, but it requires extra steps with Drush that can lead to errors and differences between environments.

## Don't Modify Production

No matter which storage you use for configuration, you should not edit your configuration in production. Instead, you should install the [config readonly](https://www.drupal.org/project/config_readonly) module in production and make all of your changes in your local environment. Clients who don't install Drupal locally can make configuration changes in development. Using a host like Pantheon makes it easy to deploy files from development to production.

## So Why Does Drupal Store Config in the DB?

I prefer keeping configuration in the file system, and BackdropCMS agrees with me. But, a few smart core developers don't see it that way. So, why not? Drupal 8 is slow. And, some poor web hosts might allow the public to read configuration files.

Early in the release cycle the install process was slow. So initially, moving configuration into the database made running the installer a bit faster. However, file-based configuration in the current release of Drupal 8 doesn't make the installer visibly slower. So, this isn't a problem for our workflow.

The second concern with file based configuration is the desire for security through obscurity. Since we are storing configuration outside the webroot, and our web server should also be configured not to display configuration files, this isn't an issue.

Another concern was that file configuration might encourage people to edit their configuration. Since this workflow is for programmers, this is an advantage of our workflow.

## Advantages of Database Config Storage

Storing configuration in the database on production has some minor advantages. So, leaving the configuration in the database on production is reasonable. Storing in the file system means you have to sync the file system in multiple web server environments.

Storing config in the database allows you to attach metadata to the configuration so that you can timestamp it, assign an owner to it and create a revision workflow for configuration.


## How to Enable Config in Files

The easiest way is to use the [Drupal8-base installer](https://github.com/vincenzodibiaggio/drupal8_base) which will enable file storage for configuration out of the box. Alternatively, you can export your site configuration from the database and then follow [these quick steps](https://www.drupal.org/node/2416555) to enable file-based configuration storage on an existing Drupal site. 
