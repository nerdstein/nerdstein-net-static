---
title: "Nodes with no page views"
date: 2013-01-01
slug: "nodes-with-no-pages"
tags: ["development", "drupal"]
description: "Nodes are the unquestioned most robust data structure within Drupal. It has widely adopted integration, e.g."
draft: false
---

## **Preface**

Nodes are the unquestioned most robust data structure within Drupal. It has widely adopted integration, e.g. Views, Features, Context, Rules, etc that make the Node a popular Drupal entity for countless use cases.

However, the default node structure comes with a lot of baggage. It has built in publication states, authoring information, and revisions. Most of the time, these features are advantageous. Others, not so much.

 

## **Nodes with no pages**

Due to the robust features available for nodes, a content type is often created for nodes that do not actually have viewable pages. Let's look at a few use cases.

 

- A content type for a Hero Slideshow. All nodes are rendered in a View, is there any use case in which someone "views" an actual page?

- Functional entity references. A content type is created to store metadata and/or attributes useful to organize functional components of a system. Other content types reference a functional content type to inherit specific system behaviors.

 

In both cases, any nodes created will automatically get pages upon node creation, but the pages serve little to no purpose. In fact, additional modules and configuration must be done to ensure pages are not accessible.

 

## **Soapbox**

In my view of the world, this is a relevant use case for a separate entity outside of the node. Yes, this entity can be content focused, but so is a product in a store, or a user profile page. Developers will opt for the node creation because it's readily available and presents the least challenges. Ideally, the usability of entity creation would attract people, but Drupal entities often require a lot of programming. As entities mature and become more understood/adopted by the masses, I'm confident the community will begin to have better options for the rapid development that can occur with nodes.

 

## **Solutions**

In essence, we need to hide pages of specific content types. Here are some options.

 

- **Content Access **- [https://www.drupal.org/project/content_access](https://www.drupal.org/project/content_access) - Set the permissions to view nodes of the content type. While this does not remove the page, it gets it out of public view.

- **Internal Nodes** - [https://www.drupal.org/project/internal_nodes](https://www.drupal.org/project/internal_nodes) - This executes an access denied when viewing nodes. It's configured by content type and also supports redirects or a 403 message.

- **Rabbit Hole** - [https://www.drupal.org/project/rabbit_hole](https://www.drupal.org/project/rabbit_hole) - Almost identical to internal nodes, but applies to all entities. This can apply to files, users, and taxonomy terms in addition to nodes.

 

 

I hope this helps!