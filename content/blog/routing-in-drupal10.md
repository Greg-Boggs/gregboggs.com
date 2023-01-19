+++
author = "Greg Boggs"
categories = ["Drupal"]
date = "2023-01-17"
draft = false
tags = ["Drupal"]
title = " Unleash the Power of Drupal 9 Routing: Create Custom Routes with Page Callbacks & Debug Like a Pro"
url = "/debugging-routing-page-callbacks-drupal10/"
menu: featured
+++


## How do I create a route with a page callback in Drupal 10?

To create a route file with a page callback in Drupal, you can follow these steps:

Create a new file in your module's src/Routing directory, named module_name.routing.yml.
In this file, define your route using the YAML syntax. An example of a basic route might look like this:

```
module_name.example:
  path: '/example'
  defaults:
    _controller: '\Drupal\module_name\Controller\ExampleController::examplePage'
    _title: 'Example Page'
```

The path key defines the URL path of the route, and the defaults key contains the page callback and page title for the route. In this example, the page callback is a method named examplePage in the ExampleController class of the module_name module.

Clear Drupal cache so the new route can be picked up by the system.

That's it! The new route should now be accessible at the URL /example and will use the specified page callback method.
You can also pass a parameter in the path, for example path: '/example/{parameter}'
and use it in the controller with $parameter = $route->getparameter('parameter')

## How do I debug a Drupal 10 routing file?

There are several ways to debug a routing file in Drupal 10, here are some examples:

Use the Devel module: The Devel module is a popular development tool for Drupal, it provides a suite of debugging tools, including the ability to view the routing information for your site. To enable this feature, you need to install and activate the Devel module, and then navigate to the "Devel" -> "Routes" page to view the routing information for your site.

Use the Drupal Console: The Drupal Console is a command-line interface for Drupal that provides a variety of debugging tools. To use the Drupal Console to debug your routing file, you can use the command drupal router:debug to view the routing information for your site.

Use the dpm() function: The dpm() function is a debugging function provided by the Devel module that allows you to print variables to the message area of the page. By adding dpm($routes) to the routing file, you can see the array of all routes.

Use the kint() function: The kint() function is also a debugging function provided by the Devel module that allows you to print variables to the message area of the page, but with more information than dpm(). By adding kint($routes) to the routing file, you can see the array of all routes and more information about the routes.

Use the browser developer tools: By using browser developer tools, you can see all the requests made by the browser and check if the routing file is working correctly.

It's important to remember that you should only use these debugging tools during development and remove them before deploying to a production environment, as they can expose sensitive information about your site.

## How do I make my route higher priority in Drupal 10

In Drupal 10, you can make a route have a higher priority than others by setting a higher weight for the route in the routing file. Here's an example of how to do this:

In your routing file, you can set the weight property for your route. The weight property is used to determine the order of the routes. Routes with a higher weight will be matched first.

```
empty_front_page.content:
  path: '/'
  defaults:
    _controller: '\Drupal\empty_front_page\Controller\EmptyFrontPageController::content'
    _title: 'Empty Front Page'
  weight: 10
```

The default weight is 0. If you want your route to have a higher priority, you can set a higher weight. In the example above, the weight is set to 10, which makes it have a higher priority than any other route with a lower weight.

Keep in mind that if you have multiple routes with the same weight, the order in which they are defined in the routing file will determine which route is matched first.

Clear the cache after making any changes in routing file.

By setting a higher weight for your route, you can ensure that it is matched before any other routes with a lower weight. This can be useful if you have multiple routes that match the same path and you want to ensure that a specific route is always matched first.

And there you have it folks, you're now a pro at creating custom routes and debugging like a boss in Drupal. Just remember, if you ever get stuck, don't hesitate to call upon the almighty Drupal gods for guidance... or just Google it. Happy routing!
