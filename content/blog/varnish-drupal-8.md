---
title: "Just Another Varnish and Drupal 8 Blog Post"
date: 2016-12-07
slug: "varnish-drupal-8"
tags: ["development", "drupal"]
description: "A practical guide to configuring Varnish 4 with Drupal 8, using the Purge module and cache tags to get proper invalidation working."
draft: false
---

Since both core caching continues to evolve in Drupal 8 and contrib modules are maturing, I wanted to capture my steps for configuring Varnish 4 to properly work with Drupal 8.

## Set up the VCL

First, I am **NOT** a systems administrator. I rely heavily on the expertise of others in the community to steer my efforts. I set up Varnish to serve up content from the Drupal site, hoping that the VCL configuration I found from Jeff Geerling would do the trick. (Reference: [https://raw.githubusercontent.com/geerlingguy/drupal-vm/master/provisioning/templates/drupalvm.vcl.j2](https://raw.githubusercontent.com/geerlingguy/drupal-vm/master/provisioning/templates/drupalvm.vcl.j2)). Under your *acl purge* IP settings in the VCL, ensure your server's IP address is listed so that the purge settings will work. And, it worked. Except, the site wasn't properly informing Varnish when it should invalidate. You can reload your Varnish config by running the *varnish_reload_vcl* command.

## Contributed Modules

Thankfully contrib saves the day. Motivated by Jeff's blog post (reference: [http://www.jeffgeerling.com/blog/2016/use-drupal-8-cache-tags-varnish-and-purge](http://www.jeffgeerling.com/blog/2016/use-drupal-8-cache-tags-varnish-and-purge)), I noticed the use of the Purge module. This is a popular module to use for Drupal 7 cache invalidation and the list of maintainers are household Drupal names. Many of the concepts used by the Purge module served as motivation for the CloudFlare module, with is immaculately maintained by my friend Adam Weingarten. And, as usual, Adam had a wealth of knowledge to add.

## Steps to Profit

Download the 8.x-3.x release of Purge and the 8.x-1.4 release of Varnish Purge.  Enable the base modules and dependencies:

*drush en varnish_purger* (pet peeve: note the subtle difference between the project page *varnish_purge* and the code *varnish_purger*).

Purge ships with a queue system and CRON integration. It also has a UI for configuration. Enable these modules as well:

*drush en purge_queuer_coretags,purge_processor_cron,purge_ui*

Configuration steps are as follows:

- Set the appropriate page cache maximum age at */admin/config/development/performance. *I find a 24 hour setting to be common, but this can be lowered based on your hardware and need.

- Add the Varnish Purger at */admin/config/development/performance/purge*. Select "Varnish Purger" and verify your Varnish configuration by clicking "Configure" next to the operations of your new purger. In the "Headers" tab of the configuration, add "Purge-Cache-Tags" header with a value of "[invalidation:expression]".

- You will note the "Core tags queuer" and "Cron processor" are displayed under "Queue". Further tuning can be made, but I leveraged the default configuration. This also applies to the logging behavior.

References: 

- [https://www.drupal.org/project/purge](https://www.drupal.org/project/purge)

- [https://www.drupal.org/project/varnish_purge](https://www.drupal.org/project/varnish_purge)

- [https://wunderkraut.se/blogg/purge-cachetags-varnish](https://wunderkraut.se/blogg/purge-cachetags-varnish)

## Testing

Again, thanks to Adam Weingarten for helping me define testing steps.

- Verify that Varnish is working (please replace your site URL annotated in the command below):
*curl -SLIXGET URL-GOES-HERE*

 You should see "X-Varnish" headers coming through, including whether Varnish reported a cache hit or miss.

- Make some content edits to invalidate a page.

- Run CRON:

 *drush cron*