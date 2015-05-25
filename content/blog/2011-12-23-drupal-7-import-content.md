---
id: 425
title: Drupal 7 Import content with custom fields, images, and taxonomy
author: Greg Boggs

guid: http://www.gregboggs.com/?p=425
url: /drupal-7-import-content/
date: 2011-12-23
categories:
  - Blog
---
I'm in the process of migrating an [old PHP website][1] for Portland State University from a custom database into Drupal 7. Doing the data entry on hundreds of nodes with multiple custom fields, taxonomies, and images would have taken ages. So, instead I imported the data into Drupal with a PHP script. At first, I attempted to use phpMyAdmin, to export a CSV, and then import the CSV using the Feeds module. However, the feeds module for Drupal 7 doesn't seem to do field matching well, and I couldn't get the taxonomies or images to import correctly. So, with the help of my intelligent coworker, I decided to use Drush to execute a PHP script that will import the content. The process wasn't hard for a PHP programmer, but all the directions I found on other blogs were either [confusing me][2], or [missing a few steps][3]. Mainly the examples were missing the code to insert dynamic data from a database in a loop.

This being my first Drupal 7 project, I had a lot to learn about new Drupal features. Don't worry, I've attached the code, so you can cut and paste my hard work.

## Import content into Drupal 7

  1. Create the taxonomies and terms that you will need. This can be done with a script, but most websites don't have that many categories.
  2. Create a content type for the nodes and include all the custom fields you will need. Be sure to include term reference fields for each taxonomy from step 1.
  3. Install Drush and get &#8220;Drush help&#8221; to work.
  4. Create a PHP script, and execute it with drush php-script (script name)

Drush is nifty because it loads the Drupal environment and allows you to access Drupal's functions. This saves you from having to figure out where to insert all the node data manually.

## Connect to the database and get content

// My source data was not normalized. All data was in 1 table! Lucky me. No joins.  


    
    $query = 'SELECT * FROM `tb|record`';
    $result = db_query($query);
    $i = 20;
    foreach ($result as $row) {
    

Most of what Tim wrote worked perfectly, but here's what Tim has to say about assigning content to categories&#8230;

> ## Add a term to a node
> 
> `$node-&gt;field_tags[$node-&gt;language][]['tid'] = 1;`  
> &#8216;field_tags' here is the name of a term reference field attached to your content type, '1&#8242; is a term id you wish to assign to a node. Simple!

Now here's the code I actually used to insert my content into a category. It wasn't simple:  


     if ( $term = taxonomy_get_term_by_name($row-&gt;culture) ) {
    $terms_array = array_keys($term);
    $node-&gt;field_culture[$node-&gt;language][]['tid'] = $terms_array['0'];
    }
    

If you review my code, you'll notice that I failed to get my loop to read and load the taxonomies from the database, so I added them one a time. If anyone can figure out the syntax error in the block of code that's commented out, that would be awesome. [Contact me][4], and I'll give you credit. But, I doubt many sites have more than a handful of categories.

The script took me about 10 hours to perfect after I threw away 2-3 different methods. Hopefully, you can copy this script and get your site converted over to Drupal in much less time.

## The Full Source Code

    
    <!--?php <br ?--> cm_load_rep_data();

function cm\_load\_rep_data( ) {

// My source data was not normalized. All data was in 1 table! Lucky me. No joins.  
$query = &#8216;SELECT * FROM \`tb|record\`';  
$result = db_query($query);  
$i = 20;  
foreach ($result as $row) {  
$node = new stdClass(); // We create a new node object  
$node->type = &#8216;piece'; // Or any other content type you want  
$node->title = $row->subject;  
$node->language = LANGUAGE_NONE; // Or any language code if Locale module is enabled. More on this below *  
$node->uid = $i; // Or any id you wish  
$url = str\_replace(&#8221; &#8220;,&#8221;\_&#8221;,$row->subject);  
$node->path = array(&#8216;alias' => $url) ; // Setting a node path  
node\_object\_prepare($node); // Set some default values.  
$i++;

//grab the file for this node based on the &#8220;schema&#8221; from the old website&#8230;  
$file\_path = &#8216;/home/gboggs/Images\_data/'  
. $row->collection_alias . &#8216;/'  
. $row->collection\_alias . $row->accession\_no . &#8216;.jpg';

if (file\_exists($file\_path)) {  
$file = (object) array(  
&#8216;uid' => $i ,  
&#8216;uri' => $file_path,  
&#8216;filemime' => file\_get\_mimetype($filepath),  
&#8216;status' => 1,  
);  
$file = file_copy($file, &#8220;public://&#8221;);  
$node->field\_image\[LANGUAGE\_NONE\]\[0\] = (array)$file;  
}

// Grab the body content. My database had the body content repeated. You don't need this piece.  
if (!isset($row->long\_des) || $row->long\_des == null) {  
$body = $row->short_des;  
} else {  
$body = $row->long_des;  
}

// Insert the content into the node  
$node->body\[$node->language\]\[0\]['value'] = $body;  
$node->body\[$node->language\]\[0\]['format'] = &#8216;full_html';

// Let's add some CCK fields. This is pretty similar to the body example  
$node->field\_collection\_number\[$node->language\]\[0\]['value'] = $row->accession_no;  
$node->field_dimensions\[$node->language\]\[0\]['value'] = $row->dimension;  
$node->field_date\[$node->language\]\[0\]['value'] = $row->date;  
$node->field\_artist\_author\[$node->language\]\[0\]['value'] = $row->artist;  
$node->field\_provenance\[$node->language\]\[0\]['value'] = $row->provenance\_prior_pub;  
$node->field\_details\[$node->language\]\[0\]['value'] = $row->object\_details;

/* This doesn't execute, and I couldn't figure out why in < 10 minutes. so doing it the long way.  
$categories = array(&#8216;field_culture' => &#8216;culture',  
&#8216;field_medium' => &#8216;medium',  
&#8216;field\_time\_period' => &#8216;time_periods',  
&#8216;field_collection' => &#8216;collection',  
&#8216;field_theme' => &#8216;theme');  
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
node_save($node); // After this call we'll get a nid

// printing from Drush is easy  
drush_print( $row->subject . &#8221; added.\n&#8221; );  
}  
}  
?>

 [1]: http://www.medievalportland.pdx.edu/
 [2]: http://shout.setfive.com/2011/02/09/drupal-7-batch-insert-nodes-with-drush/
 [3]: http://timonweb.com/how-programmatically-create-nodes-comments-and-taxonomies-drupal-7
 [4]: http://www.gregboggs.com/contact/ "Contact"