---
id: 453
title: Decode your WordPress content to UTF-8
author: Greg Boggs

guid: http://www.gregboggs.com/?p=453
url: /decode-your-wordpress-content-to-utf-8/
date: 2012-01-28
categories:
  - Blog
---
Ann Smarty recently posted an article about how scammers [ use foreign characters][1] to disguise duplicate content as unique, original content. If you've never seen this before, go read her post. It's really interesting.

No really. Read it. 

<http://www.seosmarty.com/content-scam-alert-using-foreign-characters-to-make-the-piece-look-unique/>

She had several great suggestions for catching the hidden characters, but, checking every guest post by hand is bound to fail eventually. You'll either get bored of never catching hidden content, or you'll just forget about. So, here's how you can always catch this kind of false character content the automated way:

Place this code into the functions.php file of your theme. Anywhere between <?php and ?> is fine. 

    
    // Transform foreign characters into ?
    function decode_content($content) {
    
        $content = utf8_decode($content);
    
        return $content;
    }
    
    add_filter('the_content', 'decode_content');
    

Now, whenever you publish an article with Cyrillic characters in it, the characters will be converted to UTF-8 and you'll see a bunch of question marks in the post. Below is an example taken directly from Ann's post:

> This p?st l??ks at ?ne type ?f c?ntent re-packaging: turning y?ur ?ld c?ntent int? an image

As you can see, the hidden characters have been revealed. Isn't PHP great? You could take this a step further and rewrite the characters to English, or warn the user when publishing posts with foreign characters, but that's not a single line of code.

Now back to work on my [cool WP scanner][2].

 [1]: http://www.seosmarty.com/content-scam-alert-using-foreign-characters-to-make-the-piece-look-unique/
 [2]: http://www.scanwp.com "Cool Vulnerability Scanner"