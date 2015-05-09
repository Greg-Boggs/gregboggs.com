---
id: 425
title: Drupal 7 Import content with custom fields, images, and taxonomy
author: greg
layout: post
guid: http://www.gregboggs.com/?p=425
permalink: /drupal-7-import-content/
categories:
  - Blog
---
I&#8217;m in the process of migrating an [old PHP website][1] for Portland State University from a custom database into Drupal 7. Doing the data entry on hundreds of nodes with multiple custom fields, taxonomies, and images would have taken ages. So, instead I imported the data into Drupal with a PHP script. At first, I attempted to use phpMyAdmin, to export a CSV, and then import the CSV using the Feeds module. However, the feeds module for Drupal 7 doesn&#8217;t seem to do field matching well, and I couldn&#8217;t get the taxonomies or images to import correctly. So, with the help of my intelligent coworker, I decided to use Drush to execute a PHP script that will import the content. The process wasn&#8217;t hard for a PHP programmer, but all the directions I found on other blogs were either [confusing me][2], or [missing a few steps][3]. Mainly the examples were missing the code to insert dynamic data from a database in a loop.

This being my first Drupal 7 project, I had a lot to learn about new Drupal features. Don&#8217;t worry, I&#8217;ve attached the code, so you can cut and paste my hard work.

## Import content into Drupal 7

  1. Create the taxonomies and terms that you will need. This can be done with a script, but most websites don&#8217;t have that many categories.
  2. Create a content type for the nodes and include all the custom fields you will need. Be sure to include term reference fields for each taxonomy from step 1.
  3. Install Drush and get &#8220;Drush help&#8221; to work.
  4. Create a PHP script, and execute it with drush php-script (script name)

Drush is nifty because it loads the Drupal environment and allows you to access Drupal&#8217;s functions. This saves you from having to figure out where to insert all the node data manually.

## Connect to the database and get content

// My source data was not normalized. All data was in 1 table! Lucky me. No joins.  


    
    $query = &#039;SELECT * FROM `tb|record`&#039;;
    $result = db_query($query);
    $i = 20;
    foreach ($result as $row) {
    

Most of what Tim wrote worked perfectly, but here&#8217;s what Tim has to say about assigning content to categories&#8230;

> ## Add a term to a node
> 
> `$node-&gt;field_tags[$node-&gt;language][][&#039;tid&#039;] = 1;`  
> &#8216;field_tags&#8217; here is the name of a term reference field attached to your content type, &#8217;1&#8242; is a term id you wish to assign to a node. Simple!

Now here&#8217;s the code I actually used to insert my content into a category. It wasn&#8217;t simple:  


     if ( $term = taxonomy_get_term_by_name($row-&gt;culture) ) {
    $terms_array = array_keys($term);
    $node-&gt;field_culture[$node-&gt;language][][&#039;tid&#039;] = $terms_array[&#039;0&#039;];
    }
    

If you review my code, you&#8217;ll notice that I failed to get my loop to read and load the taxonomies from the database, so I added them one a time. If anyone can figure out the syntax error in the block of code that&#8217;s commented out, that would be awesome. [Contact me][4], and I&#8217;ll give you credit. But, I doubt many sites have more than a handful of categories.

The script took me about 10 hours to perfect after I threw away 2-3 different methods. Hopefully, you can copy this script and get your site converted over to Drupal in much less time.

## The Full Source Code

    
    <!--?php <br ?--> cm_load_rep_data();

function cm\_load\_rep_data( ) {

// My source data was not normalized. All data was in 1 table! Lucky me. No joins.  
$query = &#8216;SELECT * FROM \`tb|record\`&#8217;;  
$result = db_query($query);  
$i = 20;  
foreach ($result as $row) {  
$node = new stdClass(); // We create a new node object  
$node->type = &#8216;piece&#8217;; // Or any other content type you want  
$node->title = $row->subject;  
$node->language = LANGUAGE_NONE; // Or any language code if Locale module is enabled. More on this below *  
$node->uid = $i; // Or any id you wish  
$url = str\_replace(&#8221; &#8220;,&#8221;\_&#8221;,$row->subject);  
$node->path = array(&#8216;alias&#8217; => $url) ; // Setting a node path  
node\_object\_prepare($node); // Set some default values.  
$i++;

//grab the file for this node based on the &#8220;schema&#8221; from the old website&#8230;  
$file\_path = &#8216;/home/gboggs/Images\_data/&#8217;  
. $row->collection_alias . &#8216;/&#8217;  
. $row->collection\_alias . $row->accession\_no . &#8216;.jpg&#8217;;

if (file\_exists($file\_path)) {  
$file = (object) array(  
&#8216;uid&#8217; => $i ,  
&#8216;uri&#8217; => $file_path,  
&#8216;filemime&#8217; => file\_get\_mimetype($filepath),  
&#8216;status&#8217; => 1,  
);  
$file = file_copy($file, &#8220;public://&#8221;);  
$node->field\_image\[LANGUAGE\_NONE\]\[0\] = (array)$file;  
}

// Grab the body content. My database had the body content repeated. You don&#8217;t need this piece.  
if (!isset($row->long\_des) || $row->long\_des == null) {  
$body = $row->short_des;  
} else {  
$body = $row->long_des;  
}

// Insert the content into the node  
$node->body\[$node->language\]\[0\]['value'] = $body;  
$node->body\[$node->language\]\[0\]['format'] = &#8216;full_html&#8217;;

// Let&#8217;s add some CCK fields. This is pretty similar to the body example  
$node->field\_collection\_number\[$node->language\]\[0\]['value'] = $row->accession_no;  
$node->field_dimensions\[$node->language\]\[0\]['value'] = $row->dimension;  
$node->field_date\[$node->language\]\[0\]['value'] = $row->date;  
$node->field\_artist\_author\[$node->language\]\[0\]['value'] = $row->artist;  
$node->field\_provenance\[$node->language\]\[0\]['value'] = $row->provenance\_prior_pub;  
$node->field\_details\[$node->language\]\[0\]['value'] = $row->object\_details;

/* This doesn&#8217;t execute, and I couldn&#8217;t figure out why in < 10 minutes. so doing it the long way.  
$categories = array(&#8216;field_culture&#8217; => &#8216;culture&#8217;,  
&#8216;field_medium&#8217; => &#8216;medium&#8217;,  
&#8216;field\_time\_period&#8217; => &#8216;time_periods&#8217;,  
&#8216;field_collection&#8217; => &#8216;collection&#8217;,  
&#8216;field_theme&#8217; => &#8216;theme&#8217;);  
foreach ($categories as $field => $category) {  
$term = taxonomy\_get\_term\_by\_name($row->$category);  
$node->$field\[$node->language\]\[\]['tid'] = $term->tid;  
}  
*/

// The long way to check taxonmy terms and add them to the node.  
if ( $term = taxonomy\_get\_term\_by\_name($row->culture) ) {  
$terms\_array = array\_keys($term);  
$node->field\_culture\[$node->language\]\[\]['tid'] = $terms\_array['0'];  
}

if ( $term = taxonomy\_get\_term\_by\_name($row->medium) ) {  
$terms\_array = array\_keys($term);  
$node->field\_medium\[$node->language\]\[\]['tid'] = $terms\_array['0'];  
}

if ( $term = taxonomy\_get\_term\_by\_name($row->time_periods) ) {  
$terms\_array = array\_keys($term);  
$node->field\_time\_period\[$node->language\]\[\]['tid'] = $terms_array['0'];  
}

if ( $term = taxonomy\_get\_term\_by\_name($row->collection) ) {  
$terms\_array = array\_keys($term);  
$node->field\_collection\[$node->language\]\[\]['tid'] = $terms\_array['0'];  
}

if ( $term = taxonomy\_get\_term\_by\_name($row->theme) ){  
$terms\_array = array\_keys($term);  
$node->field\_theme\[$node->language\]\[\]['tid'] = $terms\_array['0'];  
}

$node = node_submit($node); // Prepare node for a submit  
node_save($node); // After this call we&#8217;ll get a nid

// printing from Drush is easy  
drush_print( $row->subject . &#8221; added.\n&#8221; );  
}  
}  
?>

 [1]: http://www.medievalportland.pdx.edu/
 [2]: http://shout.setfive.com/2011/02/09/drupal-7-batch-insert-nodes-with-drush/
 [3]: http://timonweb.com/how-programmatically-create-nodes-comments-and-taxonomies-drupal-7
 [4]: http://www.gregboggs.com/contact/ "Contact"