---
title: "A slideshow in Drupal 8"
date: 2016-03-15
slug: "slideshow-drupal-8"
tags: ["development", "drupal"]
description: "A step-by-step walkthrough for building a slideshow in Drupal 8 using core field types and Views, with no contrib required."
draft: false
---

I thought I'd play around with creating this feature in Drupal 8. Here's the step-by-step run down. This is assumed your logged in with an administrative user.

## 1. "Slideshow Item" data structure

Create a slideshow item content type with any structure you desire. In my case, I added an image, a title, a description, and a link. This was all done by core provided field types.

- Manage > Structure > Content Types

- Add Content Type

- Fill out the form for slideshow items and Save

- Enter the fields you desire for the data structure

## 2. Slide ordering

I considered adding a weight as a numeric field. However, I opted to checkout the status of the nodequeue module. This was replaced by the [Entityqueue](https://www.drupal.org/project/entityqueue) module. I downloaded the module, enabled this module, and set up a new entity queue (under structure) for only slideshow item nodes.

- *drush dl entityqueue -y*

- *drush en entityqueue -y*

- Manage > Structure > Entityqueues

- Add Entityqueue

- Fill out the form for a slideshow queue, assign this to your content type created in the first step, save.

## 3. Interactivity

To get the actual slideshow functionality, I used the Views Slideshow module. This module, however, is just an API. I enabled the Views Slideshow Cycle module to get the cycle effect. Since this is an API, you can enable any other module for the effect you desire or leverage the API to build your own. I enabled this in the View by changing the format and selecting "cycle" as the effect.

- *drush dl views_slideshow -y*

- *drush en views_slideshow_cycle -y*

##

## 4. Slideshow rendering

 I set up a View of Slideshow Items with a block output. I set up a relationship to the specific entity queue, which afforded sorting by the order in the queue. 

- Manage > Structure > Views

- Add View

- Fill out the form for your slideshow display, select block, format Views Slideshow, click Save

- Add desired render fields, create relationship to the entityqueue, sort by the entityqueue order, configure cycle settings, and save

##

## 5. Cleanup

This gets most of the functionality working. There is a lot of tweaking of styles and settings to support your specific use case and design. For example, I had to style the controls of the slideshow, I had to tweak the image settings to match my design requirements, and I had to add classes to the View to properly annotate the markup for the styles.

## Conclusion

I know this is a simple show and tell, but wanted to highlight some subtle differences in site building from Drupal 7 to Drupal 8. Hope it helps!