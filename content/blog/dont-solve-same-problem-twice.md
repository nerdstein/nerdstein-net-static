---
title: "Don't solve the same problem twice"
date: 2013-01-01
slug: "dont-solve-same-problem-twice"
tags: ["development", "drupal"]
description: "If you spent hours solving a problem, what is the likelihood you will remember exactly what you did the next time it comes around?"
draft: false
---

If you spent hours solving a problem, what is the likelihood you will remember exactly what you did the next time it comes around? Don't solve the same problem twice. Find a way to automate routine tasks so you can focus on other challenges. What are some strategies used?

Let's start by proposing a frame of reference:

- We have **features**, representing software requirements or components

- We have **tools**, which create or support features

- We have **configuration**, which sets options or behaviors of tools for use in features

Let's consider the following example. A restaurant has content management needs for their website. They feature a menu on their site, where the chefs build the menu and the management sets the prices for the menu items. The developer sets up a data structure for the menu items and a listing on the site. The dev proceeds to create two roles: *chefs* and *managers*. They proceed to create the various users and assign roles.

The features represent the menu and it's respective workflow between chefs and managers. The tools would be the data structure, the content management system, and any plugins leveraged for the solution. The configuration would set up the access control and the workflow to support the separation of duties.

So what happens when another restaurant wants this? Do you have a simple way to rebuild this? How do we not solve the same problem twice?

Let's look at [*Drupal*](https://drupal.org), which provides some interesting considerations. What mechanisms does Drupal have to help us with this?

- **Creating or exporting code** - Drupal has a robust API to do development but also a very extensible site building interface that doesn't require code. Modules like Features help bridge the gap by exporting code from parts of the site built through the interface.

- **Scripting tools** - Drupal has a command-line tool called [*Drush*](http://drush.ws) which has the ability to perform Drupal-specific administration tasks. Consider *Drush Make*, which defines make files that contain the Drupal modules and their respective versions in a standard format. By running the make command, all of the tools are downloaded and ready to be configured.

- **Scripting configuration** - We again leverage Drush commands to perform this configuration. The most common use cases are enabling / disabling modules, running SQL commands, setting site-wide variables, user management, etc.

So, how would we build a second restaurant site? We could create a feature that outputs a Drupal module for the existing menu data structure and display. We create a Drush make file that defines the dependent Drupal modules like [*Field Permissions*](https://drupal.org/project/field_permissions) which would prohibit a chef from setting the price field in the menu item. Lastly, we create a bash or Fabric script that contains the Drush commands to set up the *chef* and *manager* roles, configure permissions for the roles, turn on the Drupal modules defined in the make file, and configure the access control.

-----

When you are building solutions, reflect on the problems you solved and how you can reuse the code in an automated fashion moving forward.