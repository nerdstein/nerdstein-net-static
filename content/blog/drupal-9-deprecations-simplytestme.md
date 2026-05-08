---
title: "Drupal 9 Deprecations with SimplyTest.me"
date: 2020-03-04
slug: "drupal-9-deprecations-simplytestme"
tags: ["development", "drupal"]
description: "Drupal 9 readiness is as easy as cleaning up deprecations for your Drupal 8 project. SimplyTest is well positioned to help with this."
draft: false
---

Drupal 9 readiness is as easy as cleaning up deprecations for your Drupal 8 project. SimplyTest is well positioned to help with this.

 

## Deprecation Reporting

You can generate a report of the deprecations by performing the following steps:

 

- Go to [simplytest.me](https://www.simplytest.me)

- Under “Enter a project name:”, start typing the name of your project and select it

- Select the relevant 8.x branch (not release, as this will also scan unreleased commits)

- Expand “Additional Options”

- Click “Add Additional Project”

- Start typing “Upgrade Status” and select it

- Click “Launch Sandbox”

- Go to “admin/reports/upgrade-status”

- Select your project

- Click “Scan”

 

This will generate a list of the deprecations. Do not close the modal or the browser tab, as we will use it later.

 

## Filing an Issue

If you are testing a Drupal.org project, file an issue against that project for the deprecations report. Upgrade Status will report back for an existing issue, but please double check that an existing issue does not exist. I used the following steps to submit the report:

 

- Go to the project page and click “file issue”

- Select the appropriate 8.x branch

- Issue title: “Drupal 9 Compatibility”

- On your reporting tab, click “Export as HTML”

- Copy the HTML source containing the table of deprecations

- Paste this into the issue description

- Click “Save”

 

## Remediation

Currently, the only way to get a completely remediated Drupal 9 project is to manually address each item found in the report. From personal experience, addressing deprecations is a drastically simpler exercise than performing a Drupal 7 to 8 port. This is primarily because Drupal 8 was a big shift off the island and now is concerned about dependencies. Architecturally, Drupal 8 changed a lot of APIs, introduced Composer, changed paradigms (e.g. procedural to object oriented), and leveraged modern design patterns. Drupal 9 leverages basically the same architecture as 8, but changed major versions primarily to remove deprecated functionality.

 

Again, while the work is manual, the task should be relatively straightforward code refactoring. And, there is good guidance. Many of the items listed in a report also link to the relevant drupal.org issue for the deprecation. This is useful to identify how to properly remediate the deprecation and offer relevant context.

 

## Automated Remediation

I expect deprecations to be the new norm as dependencies end-of-life or changes are made to core with minor releases. We can come to expect more frequent major releases that follow the same paradigm as 8 to 9. But, wouldn’t it be cool if this could be automated?

 

The [Upgrade Rector](https://www.drupal.org/project/upgrade_rector) project built by Gábor Hojtsy, based on the drupal8-rector project created by Dezső Biczó at Pronovix, aims to do just that. It aims to build off of the Upgrade Status module by automatically remediating deprecations. Each deprecation maps to a specific rector rule. These rules map deprecated code to their updated equivalents.

 

Palantir recently wrote a blog post on the Upgrade Rector project. They are actively looking for contributors to work on rector rules in [their Github project](https://github.com/palantirnet/drupal-rector). As of now, only [one rule](https://github.com/palantirnet/drupal-rector/tree/master/src/Rector/Deprecation) for “drupal_set_message” is completed, which is why this process is not yet fully automated. We all need to help get this up to 100%, if possible. Many thanks to Palantir and [this blog post discusses the project](https://www.palantir.net/blog/jumpstart-your-drupal-9-upgrade-drupal-rector?utm_content=120033669&utm_medium=social&utm_source=twitter&hss_channel=tw-24758605).

 

## Future State

Why stop there? Move the Upgrade Rector into core. New deprecations in core should mean new rector rule(s) are created and should be a gate in releasing a new deprecation in core. Build infrastructure into drupal.org to periodically scans for these deprecations, files an issue against the project if new deprecations are discovered, post patches to fix them, and fire the automated tests. While I still envision manual testing would be needed to validate the results, this basically would help keep modules maintained automatically. The beginnings of this discussion are happening [here](https://www.drupal.org/project/rector/issues/3117497).

 

## Resources

- [https://www.drupal.org/docs/9/how-to-prepare-your-drupal-7-or-8-site-for-drupal-9/deprecation-checking-and-correction-tools](https://www.drupal.org/docs/9/how-to-prepare-your-drupal-7-or-8-site-for-drupal-9/deprecation-checking-and-correction-tools)

- [https://www.drupal.org/project/upgrade_rector](https://www.drupal.org/project/upgrade_rector)

- [https://www.palantir.net/blog/jumpstart-your-drupal-9-upgrade-drupal-rector](https://www.palantir.net/blog/jumpstart-your-drupal-9-upgrade-drupal-rector)

- [https://www.drupal.org/project/rector/issues/3117497](https://www.drupal.org/project/rector/issues/3117497)

- [https://github.com/palantirnet/drupal-rector](https://github.com/palantirnet/drupal-rector)