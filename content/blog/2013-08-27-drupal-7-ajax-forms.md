---
id: 706
title: Drupal 7 AJAX Forms
author: Greg Boggs

guid: http://www.gregboggs.com/?p=706
url: /drupal-7-ajax-forms/
date: 2013-08-27
categories:
  - Blog
---
Using AJAX to update a Drupal 7 form could be easier. The documentation on this feature is [extremely verbose][1], and I had a difficult time piecing together a working example. So, here's the code to modify the values of a second field when the value of the first is selected. The code below will use the taxonomy_voc drop down to control the product model drop down values. This code does not work with field widgets that define their own AJAX.

**Wrap the field that's being controlled and add the callback and wrapper to the controller field**.

Thanks to [Anne Sturdivant][2] for her assistance in writing this code.

>     
>     /*
>      *  Implements of hook_form_alter() to update a field via AJAX.
>      */
>     
>     function hitachi_module_form_alter(&$form, &$form_state, $form_id) {
>       switch ($form_id) {
>         case 'contact_us_entityform_edit_form':
>     
>         // Wrap the field that being controlled
>         // Add the callback and wrapper to the controller field
>     
>         // Create a wrapper for the AJAX callback to populate the model
>         $form['field_product_model']['#prefix'] = '<div id="hitachi_wrapper_type">';
>         $form['field_product_model']['#suffix'] = '</div>';
>     
>         // If we are editing an existing form, we already have the values
>         if (!empty($form['taxonomy_voc'][LANGUAGE_NONE]['#default_value']) 
>             || isset($form_state['values']['taxonomy_voc'][LANGUAGE_NONE][0])) {
>           $form['field_product_model'] = _hitachi_set_model($form, $form_state);
>         }
>     
>         // Create an AJAX callback. This is the magic bit that does all the AJAX.
>         $form['taxonomy_voc'][LANGUAGE_NONE]['#ajax'] = array(
>           'callback' => '_hitachi_set_model', //Must match the function name below
>           'wrapper' => 'hitachi_wrapper_type',
>         );
>       }
>     }
>     
>     /**
>      * AJAX callback to grab all the nodes with a given term.
>      *
>      */
>     function _hitachi_set_model($form, $form_state) {
>       if (!isset($form['#after_build_done']) && isset($form_state['triggering_element'])) {
>         $product_types = array_keys($form_state['triggering_element']['#value']);
>     
>         // Populate all the product models with all the product titles from that division.
>         foreach($product_types as $product_type) {
>           $entities = _hitachi_module_get_nodes_from_tid($product_type);
>           $nodes = node_load_multiple(array_keys($entities['node']));
>           foreach($nodes as $node) {
>             $title = entity_metadata_wrapper('node', $node)->title->value();
>             $key = preg_replace('/[^a-z]/i','', strtolower($title));
>             $form['field_product_model'][LANGUAGE_NONE]['#options'][$key] = $title;
>           }
>         }
>       }
>     
>       return $form['field_product_model'];
>     }
>

 [1]: https://api.drupal.org/api/drupal/developer!topics!forms_api_reference.html/7#ajax
 [2]: http://anniegreens.com/