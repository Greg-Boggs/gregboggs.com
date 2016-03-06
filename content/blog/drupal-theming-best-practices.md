---
date: "2016-05-05T11:43:59-08:00"
title: "Drupal 8 Theming Best Practices"
author: Greg Boggs
url: /drupal-8-theming-best-practices/
categories:
  - Drupal
  - Best Practices
---
The [theming guide](https://www.drupal.org/theme-guide/8) for Drupal 8 will get you started in the basics for theming a Drupal site. But, once you've learned the basics, what best practices should you be applying to Drupal 8 themes? There are [lots of popular](https://smacss.com/book/) methods for writing and organizing CSS. The basics of CSS, of course, apply to Drupal.

* Don't get too specific
* Place your CSS in the header and JavaScript in the footer
* Organize your CSS well
* Theme by patterns, don't go top down
* Preprocess your styles

## Use configuration first

When it comes to Drupal, there are some common mistakes that happen when a front end developer doesn't know Drupal. In general, apply your classes in configuration. Do not fill your Drupal theme with custom templates like you would for WordPress. Template files, especially with Twig, have their place. But, configuration should be your primary tool. My favoriate tool for applying classes is [Display Suite](https://www.drupal.org/project/ds) and [Block class](https://www.drupal.org/project/block_class). Panels is also good. And, [fences](https://www.drupal.org/project/fences) isn't terrible. 

By applying your classes in configuration allows you to easily edit, reuse, and apply classes across every type of thing in Drupal. If you apply your classes with templates, it's difficult to apply them across different types of content without cutting and pasting your code. However, don't be afraid to use some presentational logic in your Twig templates.

## Be careful what you target

In Drupal, there are many times where the only selector you have that will work is an ID. If you have this problem, Don't use it! Never, ever, ever, apply your CSS with ids in Drupal. This is true for every framework, but in Drupal it's a bigger problem because IDs are *not* reusable, they are hard to set, and they often change. A backend developer will not be able to apply your styles to other items without fixing your CSS for you. Don't write CSS that you know a PHP programmer will have to rewrite because you don't want your PHP programmer writing CSS.

## Use view modes

Make sure to target your styles to reusable elements. So, avoid node types because those aren't reusable on other nodes. Instead, use view modes and configuration to apply selectors as you need them. 

## Avoid using machine names

This relates back to avoiding IDs. Machine names in Drupal sometimes need to change, and they are not reusable. So, don't target them. Instead use view css, block class and configuration to apply classes to your content.

## Don't get too specific

Drupal 8 markup is better, but Drupal is still very verbose. Don't get sucked in by Drupal's divs. Only get as specific as you need to be. Don't replicate Drupal's HTML in your CSS.

## Apply your grid to Drupal

Choose a grid system that allows you to apply the grid to any markup like Singularity or Neat. While you certainly can Bootstrap Drupal. Using Bootstrap on Drupal requires a heavy rewrite of the HTML which will break contributed modules like Drupal Commerce in  obscure, hard to fix ways.

## Use a breadcrumb module

Do not write advanced business logic into your theme templates. If your theme is programming complex features, move that code to a module. Or, install modules like [Current Page Crumb](/drupal8-breadcrumbs/), or [Advanced Agg](https://www.drupal.org/project/advagg) to handle more complex functions. This isn't WordPress, your theme shouldn't ship with a custom version of Panels.

## Don't hard code field names or layouts

Use {{ content }} in your templates and let the View Modes, Display Suite, or Panels handle your layouts.

## Don't use template.php

If you need some 'glue', write or find a module meant for it. Drupal is built by many, many tiny modules. Learn to love it  because well-written modules are reusable, maintained for free and always improving. Custom code dropped into your theme makes for hard to maintain code.