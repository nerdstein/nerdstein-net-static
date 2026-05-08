---
title: "Removing Site Building From Drupal's Vocabulary"
date: 2017-05-23
slug: "removing-site-building-drupals-vocabulary"
tags: ["development", "drupal", "people"]
description: "Drupal has a full vocabulary of Drupalisms."
draft: false
---

Drupal has a full vocabulary of Drupalisms. While I think that is fine for Drupal-specific features, it also is a sign that we seem to promote our own island when there are similar concepts that exist in the technology space. When possible, we should try to align with more conventional terms that others outside of Drupal understand. If anything, this can make Drupal more approachable and better understood in broader context. I think I identified one such term: the term "Site Building" has never sat well with me - both as an activity and as a role. 

 

Site Building is an activity generally performed by engineers. It's technical but differs from backend or front end programming in that it doesn't necessarily involve code. The term "site" seems no longer relevant, as many Drupal implementations have broadened that context to serve purpose closer to systems and applications. This seems especially true of those instances of headless Drupal. The term "building" seems apt for the activity but less relevant as to what that activity is accomplishing. To this end, what are others in the technology space doing?

 

To level set, site building most closely resembles** System Configuration** found in other systems. And, this makes way more sense to me as a concept. Why? Individuals log into Drupal's administrative console and alter Drupal's system configuration. The byproduct of this is specific system configuration which can be output as YML (Drupal 8) or Features (Drupal 7). Drupal maintains constructs for both importing and exporting this configuration through active and passive configuration states and through it's administrative UI and command line tool Drush (continuous integration purposes). This mirrors other enterprise systems capable of changing, exporting, and deploying configuration. Such conventions also help with change management and auditing, which have well documented standards around configuration management.

 

What do you think? Should we as a community drop the term Site Building and replace with System Configuration? Hit me up on Twitter (@n3rdstein) and let's start a discussion.