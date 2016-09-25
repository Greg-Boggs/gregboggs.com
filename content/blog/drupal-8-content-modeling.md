---
date: "2016-09-25T11:43:59-08:00"
title: "Content Modeling in Drupal 8"
author: Greg Boggs
url: /drupal-8-content-modeling/
categories:
  - Drupal
  - Best Practices
menu: featured
---
In many modern frameworks, data modeling is done by building out database tables. In Drupal, we use a web-based interface to build our models. This interface makes building the database accessible for people with no database experience. However, this easy access can lead to overly complex content models because it's so easy to build out advanced structures with a few hours of clicking. It's surprising how often Drupal developers are expected to be content modeling experts. Here's a well-written [overview of content modeling](http://alistapart.com/article/content-modelling-a-master-skill) for the rest of us who aren't experts yet.

## Data Modeling Goal

Our goal when modeling content in Drupal is build out the structure that will become our editor interface and HTML output. We also need to create a model that supports the functionality needed in the  website. While accomplishing this, we want to reduce the complexity of our models as much as possible. 

## Getting Started

One of the first things to do when building a Drupal site is to build content types. So, before you start a site build, start with either a content model or a detail page wireframe. This [spreadsheet from Palantir](https://docs.google.com/spreadsheets/d/15htLLWLguhwiuTLg_nndQNpgWVdUMy6UaR_d1q-v6iw/edit#gid=0) will help you. The home page design may look amazing, but it's unhelpful for building out content types. Get the detail pages before you start building.

## Why Reduce Complexity?

The more content types you create, the more effort it will take to produce a site. Further, the more types you have, the more time it will take to maintain the site in the future. If you have 15 content types and need to make a site-wide change, you need to edit 15 different pages. 

The more pages you need to edit, the more mistakes you will make in choosing labels, settings, and formatters. Lastly, content can't easily be copied from one type to another which makes moving content around your site harder when there are many content types. So, the first thing you'll want to do with your content model is to collapse your types into as few types as feasible. How many is that?

## 5 Content Types is Enough

Drupal has many built in entities like files, taxonomy, users, nodes, comments, and config. So, the vast majority of sites don't need any more than 5 content types. Instead of adding a new content type for every design, look for ways to reuse existing types by adding fields and applying layouts to those fields.

## Break Up the Edit Form

Drupal 8 allows you to have different form displays for a single content type. With either [Form Mode Control](https://www.drupal.org/project/form_mode_control) or [Form Mode Manager](https://www.drupal.org/project/form_mode_manager), you can create different edit experiences for the same content type without overloading the admin interface.

Now that we've got the goal in mind and some tools to get us there, we'll dive into the specifics of configuring field types such as hero images and drop down lists in my next post. 