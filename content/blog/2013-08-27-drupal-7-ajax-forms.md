---
id: 706
title: Drupal 7 AJAX Forms
author: greg
layout: post
guid: http://www.gregboggs.com/?p=706
permalink: /drupal-7-ajax-forms/
date: 2013-08-27
categories:
  - Blog
---
Using AJAX to update a Drupal 7 form could be easier. The documentation on this feature is [extremely verbose][1], and I had a difficult time piecing together a working example. So, here&#8217;s the code to modify the values of a second field when the value of the first is selected. The code below will use the taxonomy_voc drop down to control the product model drop down values. This code does not work with field widgets that define their own AJAX.

**Wrap the field that&#8217;s being controlled and add the callback and wrapper to the controller field**.

Thanks to [Anne Sturdivant][2] for her assistance in writing this code.

>     
>     /*
>      *  Implements of hook_form_alter() to update a field via AJAX.
>      */
>     
>     function hitachi_module_form_alter(&$form, &$form_state, $form_id) {
>       switch ($form_id) {
>         case &#039;contact_us_entityform_edit_form&#039;:
>     
>         // Wrap the field that being controlled
>         // Add the callback and wrapper to the controller field
>     
>         // Create a wrapper for the AJAX callback to populate the model
>         $form[&#039;field_product_model&#039;][&#039;#prefix&#039;] = &#039;<div id="hitachi_wrapper_type">&#039;;
>         $form[&#039;field_product_model&#039;][&#039;#suffix&#039;] = &#039;</div>&#039;;
>     
>         // If we are editing an existing form, we already have the values
>         if (!empty($form[&#039;taxonomy_voc&#039;][LANGUAGE_NONE][&#039;#default_value&#039;]) 
>             || isset($form_state[&#039;values&#039;][&#039;taxonomy_voc&#039;][LANGUAGE_NONE][0])) {
>           $form[&#039;field_product_model&#039;] = _hitachi_set_model($form, $form_state);
>         }
>     
>         // Create an AJAX callback. This is the magic bit that does all the AJAX.
>         $form[&#039;taxonomy_voc&#039;][LANGUAGE_NONE][&#039;#ajax&#039;] = array(
>           &#039;callback&#039; => &#039;_hitachi_set_model&#039;, //Must match the function name below
>           &#039;wrapper&#039; => &#039;hitachi_wrapper_type&#039;,
>         );
>       }
>     }
>     
>     /**
>      * AJAX callback to grab all the nodes with a given term.
>      *
>      */
>     function _hitachi_set_model($form, $form_state) {
>       if (!isset($form[&#039;#after_build_done&#039;]) && isset($form_state[&#039;triggering_element&#039;])) {
>         $product_types = array_keys($form_state[&#039;triggering_element&#039;][&#039;#value&#039;]);
>     
>         // Populate all the product models with all the product titles from that division.
>         foreach($product_types as $product_type) {
>           $entities = _hitachi_module_get_nodes_from_tid($product_type);
>           $nodes = node_load_multiple(array_keys($entities[&#039;node&#039;]));
>           foreach($nodes as $node) {
>             $title = entity_metadata_wrapper(&#039;node&#039;, $node)->title->value();
>             $key = preg_replace(&#039;/[^a-z]/i&#039;,&#039;&#039;, strtolower($title));
>             $form[&#039;field_product_model&#039;][LANGUAGE_NONE][&#039;#options&#039;][$key] = $title;
>           }
>         }
>       }
>     
>       return $form[&#039;field_product_model&#039;];
>     }
>

 [1]: https://api.drupal.org/api/drupal/developer!topics!forms_api_reference.html/7#ajax
 [2]: http://anniegreens.com/