---
title: Improving Drupal Frontend Performance
date: 2014-01-19
id: 750
author: Greg Boggs
guid: http://www.gregboggs.com/?p=750
url: "/drupal-frontend-performance/"
categories:
- Drupal
menu: featured
---

Steve Sounder's is an [authority on web performance][1]. He writes about everything from front end performance to browser performance. As a front end developer, it's easy to get lost in tasks that don't matter. There's a saying in software development, "Don't optimize until you need to." In frontend development, that doesn't apply because we don't write complex algorithims. But, it's important to make sure we focus our time and attention on the right stuff. So, what is the right stuff.

The best practices to focus on as a front end developer are the ones that have the most impact on site performance and user preception. To that end, here's 4 topics that you should put special effort into:

  * Prevent jerky, flashy page loads. Restyling content after page loads is annoying and interrupts reading content.
  * Javascript, CSS and images should be minimised and compressed.
  * Images should be responsive and only as large as they need to be.
  * JavaScript and third party content should only load as needed and shouldn't cause your site to fail or delay.

## CSS at the Top

Load CSS at the top of head and JavaScript at the bottom of body. Putting all your CSS in a file at the top of the document prevents any unstyled elements from loading. Avoid inline CSS and printing CSS in JavaScript. Lastly, put your JavaScript in the footer so visitors can read the content of your website while your scripts are loading. If you can't put your animations in the footer, use a loading graphic.

## Prevent Flash of Unstyled Text

Preventing FOUT is a quick and easy win. Firefox and Internet Explorer both do a terrible job loading @font tags. These browsers cause the original unstyled text to flash, sometimes for a couple of seconds before the page is redrawn. This affect can even break your layouts on a page that uses thin custom fonts. All that's needed is adding a [bit of JavaScript][2] when you include custom fonts:  


    <script src="//ajax.googleapis.com/ajax/libs/webfont/1.4.7/webfont.js"></script>
    <script>
    WebFont.load({
    google: {
    families: ['Droid Sans', 'Droid Serif']
    }
    });
    </script>
    
## Grunt to Compress, Minify and Optimize

Grunt [automates your workflow][3] so that you never forget to put your SASS into production mode again. It allows to string together tools so you can combine, minify, and compress your static files, and optimize your images. You just type Grunt build and Grunt works it's magic. These tools can easily save you 500KB on a large project.

## Responsive Images Done Well

If you're loading a 1400 pixel hero image on a 320 pixel smart phone, your page load is going to suck. Instead, use tools like [Borealis][4] or [Picture][5] to load the best size image for the visitor. Converting a slide show to responsive images can easily save 400KB. That's a huge win.

## Prevent Single Point of Failure

Modern websites almost always include JavaScript from Facebook, Twitter, Google, LinkedIn, AddThis, Discuss and other sources. If done incorrectly, these third party scripts can each cause your page to white screen. To avoid this is simple. You should always use asynchronous snippets. If you don't have an Async snippet, then place the JavaScript just above the footer.

## CDN Saves the Day

If you use Cloud Flare as a [free content delivery network][6], Cloud Flare will compress and minify all your code and html. It will combine all your CSS and JavaScript and it will asynchronously load all of your JavaScript. All you have to do is set up Cloud Flare which takes only a few minutes. When you do switch to CF, you'll want to [exclude your web font loader][7] and any other critical javascript from the &#8220;Rocket Loader&#8221; so it doesn't get loaded last.

So, load your fonts well, clean up your code, correctly load images, and move all your JavaScript to the footer, or just use Cloud Flare and forget about performance.

 [1]: http://stevesouders.com/
 [2]: https://github.com/typekit/webfontloader
 [3]: http://www.grunt.js/
 [4]: https://drupal.org/project/borealis
 [5]: https://drupal.org/project/picture
 [6]: https://www.cloudflare.com/
 [7]: https://support.cloudflare.com/hc/en-us/articles/200169436--How-can-I-have-Rocket-Loader-ignore-my-script-s-in-Automatic-Mode-
