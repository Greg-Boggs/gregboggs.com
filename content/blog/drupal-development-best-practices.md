---
date: "2016-01-20"
title: "Drupal 8 Development Best Practices"
author: Greg Boggs
url: /drupal-development-best-practices/
categories:
  - Blog
---
These core concepts apply to Drupal site builds, and often apply to the other major web framework from WordPress to Node projects. Many of these ideas are [documented on Drupal.org](https://www.drupal.org/best-practices) as well. I'm rewriting them here because I disagree with the documentation in several key areas.

# Use The Same Development Environment
Everyone on your team should have exactly [the same development environment](http://www.drupalvm.com/). Using the same development environment ensures that the project runs exactly the same for each team member working on a project. You can do this with Vagrant, Ansible, or a Brew script.

# Backups? Put The Database in Code With CMI
Configuration Management in Drupal 8 allows you to quickly and easy store all database settings in code. Further, content should come from a single reusable source. We use Google Docs API, others use Profiler. The key is keep your test content in a shared, predictable place.

Drupal.org recommends that you backup your files and database. Since all of your code is on Github, and your database is in your code, Backups only matter in production. After a project launches, your hosting company should be providing backups. If your host isn't taking care of this automatically for you, then switch to a web host like Pantheon, WP Engine, or Site Ground. Both provide automated backups. Site Ground gives you per file recovery while Pantheon focuses on CMS backups for code/files/database in an easy to restore tool.

# Never Hack Core (or Contrib)
Don't change the framework. Instead, write your own code as a module. Pantheon, doesn't follow this rule, and it creates a lot of extra work for them. But, they have an entire company of developers to maintain their fork of Drupal. The rest of us should stick to the official release. This is true no matter the framework you're in. If you hack WordPress, your project will fail during automatic updates!

# Use Test Sites
Your hosting company should be providing 2-3 sites for each production site automatically. If your hosting company doesn't give you test sites, switch to Pantheon or WP Engine. You should make all your changes in your local environment first, test them locally, and then deploy them to test in production servers on a test server.

# Use Configuration Before Code
Instead of hard coding a class or a snippet of logic into a theme, set these values in configuration and then apply the configuration with code. This allows your code to change in the future without being rewritten. This also leads us to choose high quality, well maintained modules to build our sites out of which many people avoid. However, avoiding contributed modules means you end up rewriting basic Drupal features in every new project. Reusing code is one of the most basic steps in writing good software because reusable code will have fewer bugs and more features.

# Avoid too many modules
For those of us who work on large scale Drupal sites, we've learned that hundreds of modules can  work together to produce an amazing, large-scale software project. When building enterprise Drupal sites, it's more important to avoid using 1 poor module than it is to avoid 30 well built modules.

## This includes your custom modules
Drupal.org only talks about contributed modules, but this too many modules advice holds for custom modules as well. The more custom modules you write, the more work it takes to maintain and modify your website. Instead of writing a large collection of custom modules, or a single giant glue module, consider publishing your modules on Github. This will encourage you to create reusable code that has configuration needed to make them reusable and future proof. If your developer isn't creating open source modules along with your site builds, consider working with new developers. 

Instead of writing a massive "glue" module, break up functionality into reusable modules and use configuration to apply advanced functionality so that each module is more powerful and easier to modify without rewriting the code. 

# Follow Coding Standards

You can automatically check and repair your code for Drupal with [Code Sniffer](https://www.drupal.org/node/1419988)

Up next, Theming Best Practices for Drupal 8. 