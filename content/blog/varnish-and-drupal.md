---
title: "Varnish and Drupal"
date: 2013-01-01
slug: "varnish-and-drupal"
tags: ["development", "drupal"]
description: "How Varnish works as a reverse proxy cache for Drupal, with VCL configuration examples for handling anonymous and authenticated traffic."
draft: false
---

Drupal is a complex and robust system. Due to all of the processing required to bootstrap Drupal, enabled modules, enabled themes, and page-specific rendering, one can imagine performance becomes a major concern.

There are two primary ways of caching: a cached version of a page (***passive caching***) and back-end optimization (***active caching***). Varnish serves as a passive cache, having to rebuild itself once page content changes. This is common practice, as caching often has an expiration. The expiration can be an amount of time for automatic rebuilding of content, or can be triggered manually (like, when someone edit's a page and that page in the cache has then expired).

From a high level, Drupal renders two types of content: ***static*** and ***dynamic***. Static can be classified as generic page content (homepage, "about us", or "my team") found in Drupal node content. Dynamic content is more unpredictable. Such examples include data collection forms, parsing web service data from external sites, or administrative pages. The most common use-case for dynamic content is administrative tasks in which an ***authenticated user is updating or configuring the site***. As such, most passive caching solutions focus on ***anonymous*** ***traffic that authentication tokens do not exist***.

Varnish and Drupal solutions have been well adopted. Varnish serves as a reverse proxy to Drupal, which scrapes Drupal content and performs the functions of a passive cache.

Each Varnish instance has it's own configuration stored in VCL files. Drupal-specific VCL files are well documented (see an example here: [https://fourkitchens.atlassian.net/wiki/display/TECH/Configure+Varnish+…](https://fourkitchens.atlassian.net/wiki/display/TECH/Configure+Varnish+3+for+Drupal+7)). VCL files have the capability to specify path-specific excludes for paths that identify dynamic areas of Drupal, like administrative pages and the login screen. Furthermore, VCL files have the ability to define how Drupal sessions are processed within Varnish. This makes it possible to distinguish between anonymous and authenticated traffic.

There are many Drupal-specific modules that interface between the two systems. The Varnish module ([http://drupal.org/project/varnish](https://drupal.org/project/varnish)) provides a generic expiration module configurable through Drupal. The Expire ([https://drupal.org/project/expire](https://drupal.org/project/expire)) and Purge ([https://drupal.org/project/purge](https://drupal.org/project/purge)) modules are better for system-level events like changing content.

As the documentation for the Varnish module specifies, Drupal 7 has the ability to support multiple caching systems simultaneously. This is advantageous for splitting out specific caches Drupal maintains. One common use-case is to use Drupal's default cache for forms (bypassing Varnish). This is easily implemented in Drupal's setting file (after installing the Varnish module) by specifying a few lines of code:

```

*$conf['cache_backends'][] = 'sites/all/modules/varnish/varnish.cache.inc';

$conf['cache_class_cache_page'] = 'VarnishCache';

$conf['cache_class_cache_form'] = 'DrupalDatabaseCache';*
```

As you can see, there are many constructs that enable Drupal and Varnish to play nice in the sandbox. This is a great way to speed up your Drupal site, check it out!

**References:**

[http://www.acquia.com/blog/explaining-varnish-beginners](http://www.acquia.com/blog/explaining-varnish-beginners)

[http://www.vmirgorod.name/blog/tuning-drupal-performance](http://www.vmirgorod.name/blog/tuning-drupal-performance)

[http://www.acquia.com/blog/when-and-how-caching-can-save-your-drupal-si…](http://www.acquia.com/blog/when-and-how-caching-can-save-your-drupal-site)

[http://blogs.osuosl.org/gchaix/2009/10/12/pressflow-varnish-and-caching/](http://blogs.osuosl.org/gchaix/2009/10/12/pressflow-varnish-and-caching/)

[http://www.wunderkraut.com/blog/caching-with-varnish-drupal-7-and-cache…](http://www.wunderkraut.com/blog/caching-with-varnish-drupal-7-and-cache-actions/2012-01-31)