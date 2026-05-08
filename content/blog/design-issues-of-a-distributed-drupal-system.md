---
title: "Design issues of a distributed Drupal system"
date: 2013-01-01
slug: "design-issues-of-a-distributed-drupal-system"
tags: ["development", "drupal"]
description: "Scale and performance are major issues for high traffic websites."
draft: false
---

Scale and performance are major issues for high traffic websites. The design of the Drupal system poses many challenges to building a distributed system that can support load balancing.

 

In Drupal, the design of the system has three principle components: code, database, and files. I will be sharing potential solutions in later blog posts.

 

**Code**: This includes Drupal core and the modules that run on the web server. By running multiple web servers, you need to ensure the code is consistently maintained during deployments across all of the servers (see: continuous integration). 

The issue of timing becomes important, as you need to simultaneously update multiple web hosts at once in a load-balanced environment. An additional issue resides in the deployment practices, as you need to have stronger guarantees about deploying the same code to all machines.

**Database**: Although Drupal 8 moves configuration out of the database, versions 6 and 7 leverage the database to store node content and system configuration. This is in contrast to CMS systems that leverage deployment models from one content authoring server out to one or more web servers. One Drupal server, traditionally, serves as both the system for authoring and rendering.

This poses challenges to the common model of running a web server and database server on one host, as multiple hosts would introduce syncronization issues between content and configuration across hosts. As such, it's important to evaluate the actions performed by the database server - namely *reading* and *writing* operations. 

**Files**: While most content is stored in the database as field values of a node, file content is stored on the web server's file system in a specific Drupal directory. As such, it faces similar authoring issues to database content and similar syncronization issues to the code files. For example, consider a content provider that uploads a file to a node when authoring on one server.

 

 

Understanding these three design issues has to be at the forefront of any distributed Drupal system architecture. I will look at solutions for each component individually in upcoming blog postings.