---
title: "Site Updates in Drupal"
date: 2016-03-03
slug: "site-updates-drupal"
tags: ["development", "drupal"]
description: "Site updates in Drupal are one of the most critical, proactive things needed to eliminate vulnerabilities on your site."
draft: false
---

Site updates in Drupal are one of the most critical, proactive things needed to eliminate vulnerabilities on your site. While the open source community strives to make these updates smooth, there are no guarantees there won't be issues for your specific site based on how you've extended your Drupal instance. This is because each site may have it's own custom code, it may have it's own combination of contributed modules with unique interactions, and it may have it's own visual theme. The key point is that it's not a safe assumption that site updates meet all use cases. Most module maintainers are good about following module version conventions intended to help shed light on if an update could break existing feature or API parity. But, case in point, site updates should be handled with care. 

 

## What are some best practices?

- You can reduce risk and downtime by having the right tools on both your local system and your production system. If your not using Drush to afford scripting, Drush Aliases to manage local and remote connectivity, or Git to version code changes, you are missing fundamental tools that are widely regarded as best practice. Larger enterprise projects emphasize automated testing for your own user stories, which can also be scripted or integrated with a broader continuous integration solution (Jenkins/TravisCI, etc).

- Follow a set of conventional steps and adjust your own based on what you learn. A good starting point for all deployments is outlined by the Dcycle folks ([http://dcycleproject.org/blog/44/what-site-deployment-module](http://dcycleproject.org/blog/44/what-site-deployment-module) under the "Incremental Deployments" section). I have replaced the *drush updb -y* call with *drush up -y*, as this will perform a database update thereafter. And, when repeating on production, I always backup my code, files, and database before I start the script. The database can be saved from running *drush @PRODUCTION sql-dump > /scripts/SITE-DB-TIMESTAMP.sql.*

- Site updates should be **performed locally first**, smoke tested, and then deployed to production. One could argue that anything would work besides a production environment. But, this is only partially true. If the updates are performed locally, you can conveniently make any code updates that can be pushed up to a non-production environment later for validation. And, local updates do not require a multi-environment hosting infrastructure, just a production system. Here is [my local setup](https://nerdstein.net/blog/common-drupalvm-use).

- Each update (and deployment) should be scripted to track any manual steps needed. This should start with the aforementioned conventional steps and should expand as you smoke test a deployment and address gaps. This can include enabling of additional modules, disabling of modules, configuration changes not in code, etc.

- Perform site updates at short time intervals. It is far more likely there will be issues and substantially harder to track down when there is a substantial amount of updates to perform. This basically is a guarantee for a high number of database updates and functionality improvements/changes at once. A large quantity of updates can be very time consuming to test in depth and complicates module dependencies by the order in which updates are executed.

- Pull your content directly from production. Get **one** database archive when you start your local site upgrade process. This can be run by using *drush @PRODUCTION sql-dump > /scripts/SITE-DB-TIMESTAMP.sql*, in which the capital letters represent tokens for your use case. Do not repeatedly use *drush sql-sync*, as this wastes time and burdens the production server unnecessarily. You may be inclined to run this consecutively if you run into issues and want to re-test a production database copy. There likely will not be that many database changes between syncs, so I have found the sql-dump to be adequate and can be iterated easily with a *drush @LOCAL sql-drop* and a subsequent *drush @LOCAL sql-cli < /scripts/SITE-DB-TIMESTAMP.sql*.

- Restore production sites if there happens to be an issue that wasn't present on your local. Copy the code back over and restore the database backup by running *drush @LOCAL sql-cli < /scripts/SITE-DB-TIMESTAMP.sql*. The steps you have taken should make this a rare instance, since you are working locally.

 

## What are some practices you should avoid?

- Do not manually move databases around if you move from a local system back up to a production system. Why might you do this? This is common when you have a production host that is not equipped with SSH, Drush, or other common tools that make updates painless. You run the risk of bringing in local testing, you lose the integrity and potentials gaps in site logging (if your using DBLog), and lastly your content authors may be making content changes. Run the updates on the respective servers using the script.

- A popular strategy is to wait only for security updates to core and/or contrib. Or, to only make security updates. I find this approach problematic for the same reasons of the previous point. Other updates will continue to stagger, increasing the amount of differences you will bring in later (and potentially introduce problems). Security updates should be as immediate as possible. Full code updates should still be done on a regular interval.

- When you run into issues, it's common practice to just hack around and get it to work. That's fine! But don't hesitate to revert from a backup, post an issue to drupal.org, and create a patch that can be used for others that may have the issue. Or, if your not a coder, someone else may pick it up and you could use it to re-run the updates effectively.

- Avoid old-school tools like FTP, PHPMyAdmin, and others that may slow down or complicate this process. Bear in mind, the less time you spend down, the happier the customer is. Drush completely replaces the utility provided by both tools. But, some Windows-based or simple Linux hosting providers often do not ship with Drush by default. If not, see if you can get it installed. And, if you are worried about this, consider moving to a host that may provide more readily available tools.

##

## Summary

Much of this process is removing the guesswork and putting some standard process in place. It's not overly complex, especially if you have the right tools at your disposal.