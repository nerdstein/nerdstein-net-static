---
title: "Theming Drupal 8 Field Collections"
date: 2016-07-01
slug: "theming-drupal-8-field-collections"
tags: ["development", "drupal"]
description: "I'm a big fan of Field Collections."
draft: false
---

I'm a big fan of Field Collections. It provides a high level of flexibility in setting up an auxiliary (and potentially shared) data structure that can associate with another entity. As such, it's a highly customizable way to do relational data in Drupal. This shouldn't be confused with Inline Entity Form which helps embed an entity within another entity (and is also an amazing project).

 

One of the major challenges is around the fact that the Field Collection entity is decoupled from the entity in which it is hosted. This complicates practically everything from rendering, Views, and much more. One such area is theming. Drupal 8 certainly helps with all of this, but the 8.x-1.x version of Field Collection still suffers from the usability of this decoupling and a lack of documentation (as most 8.x projects do).

 

I went on a quest to determine how to theme a custom Slideshow block type that I built with a Field Collection field. The block has a series of metadata fields (title, description, and set of fields that control behavior) and the field collection to manage the "slides" (a title, body, link, and the background image). I spent hours trying to figure out how to do this and thought it was best to capture this within a blog post for others to profit from.

 

First, I haven't found a Drupal-sponsored block type template. In Drupal 8, there is the concept of custom block types and they are fieldable in Drupal 8, but, sadly no templates that back that up. I spent hours looking into this issue and crafted a small block of code I've been using to create a consistent naming convention for standard block type templates.

 

The following code goes into the theme's yourtheme.theme file:

``

/**

 * Override block theme suggestions.

 *

 * @param $suggestions

 * @param $variables

 */

function yourtheme_theme_suggestions_block_alter(&$suggestions, $variables) {

  $content = $variables['elements']['content'];

  $block_types = array(

    'your_banner_image',

    'your_four_corners',

    'your_map',

    'your_sidebar_basic',

    'your_sidebar_with_image',

    'your_slideshow'

  );

  if (isset($content['#block_content'])

    and $content['#block_content'] instanceof\Drupal\block_content\BlockContentInterface

    and in_array($content['#block_content']->bundle(), $block_types)) {

    $suggestions[] = 'block__block_content_' . $content['#block_content']->bundle();

  }

}

 

If I have a "your_slideshow" custom block type, I would then have a corresponding template file "block__block_content_your_slideshow.html.twig" file.

 

Now that we have a template for this block type, we need to render the fields and markup in Twig. Most fields are rendered as *{{ content.field_name }}* or some attribute like *{{ content.field_name.value }}* . Out of the box, Field Collections have very limited wholesale render options as "full entity" or "fields". None of these were particularly useful for building a finely-tuned markup with Field Collection data. Especially if you are trying to create markup specific to the block type. An alternative could be a View Mode and it's own template, but this is a larger technical lift then coding the Twig template directly. Or, so I thought.

 

After hours of researching and hacking, I finally came up with a solution.

 

``

{% for slide in content.field_slides['#items'] %}
![]({{ file_url(slide.getFieldCollectionItem().field_background_image[0].entity.uri.value) }})
       data-cycle-title="{{slide.getFieldCollectionItem().field_title.value}}"

       data-cycle-desc="{{slide.getFieldCollectionItem().field_body.value}}
[{{slide.getFieldCollectionItem().field_button.title}}]({{slide.getFieldCollectionItem().field_button.url}})"/>

{% endfor %}

 

That solution leverages Drupal's Twig function *getFieldCollectionItem()* which retrieves the fields from the field collection. These fields can then be rendered like other fields in Twig.

 

I hope this saves some other folks time, as it took me way too long to determine how to do this.