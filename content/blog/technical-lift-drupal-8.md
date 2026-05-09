---
title: "The Technical Lift of Drupal 8"
date: 2016-07-27
slug: "technical-lift-drupal-8"
tags: ["development", "drupal", "people"]
description: "Drupal 8 has been widely praised for improving the developer experience (DX)."
draft: false
---

Drupal 8 has been widely praised for improving the developer experience (DX). The "best of breed" adoption of tools (see: Symfony, Guzzle, PHPUnit, Composer, etc) clearly positions Drupal to mature and evolve beyond that which one community is able to do alone. But, there are many different considerations of DX that need explored. And, what lift is required for the community to grasp this new version? And, what is the impact?

## DX Considerations

Probably the number one thing that is praised with Drupal 8 is the technical modernization. Drupal is already challenging to learn effectively. But, if you need to learn, you should learn modern best practices. Drupal 7 is largely procedural, while the PHP community has long since moved toward object-oriented. Open source projects confirm this movement (see: Symfony) and developers reap the benefits of class autoloading, name spacing, and incredible new features (plugin system, event subscribers, etc). Development now has better defined best practices that follow OO design patterns and not design patterns established just for Drupal (based on hooks, runtime prioritization, and complex module interoperability). 

With improvement comes drawbacks (yes! even to DX).

## CMI / Features / Multi Environment

A major feature of Drupal 8 is a built-in configuration system. Yes - this was direly needed as a foundational part of Drupal and establishing best practices around it. Having configuration in code is widely regarded as best practice. But, who used it? Large enterprise development teams doing development in parallel, having strict CI processes, and finely tuned DevOps practices. Smaller teams often lack the tools in the infrastructure or time to do this effectively, but they now need near real time access to Drupal's configuration. Formerly, it was only Drupal's content that had this requirement (when/if developers wished to pull down refreshed content was more or less at their discretion and wasn't as impactful to most development needs). 

What approaches do developers have at their disposal:

- Leave "manual" steps in a ticket to perform actions within each environment.

- Leverage the Drupal UI Configuration Synchronization in each environment for a "copy/paste" style workflow.

- Leverage the Drupal UI to do a full import / export across environments.

- Leverage a code repository for synchronizing the full configuration across environments.

Let's explore each one briefly:

**Approach 1** - This is hugely time consuming and error prone. But, it completely separates configuration by environment and avoids the need to synchronize this configuration. But, how can you test the impact to production if the configuration in each environment wasn't in sync?

**Approach 2** - This is the same as approach 1, but leveraging the configuration management system.

**Approach 3** - This improves approach certainly improves on approach 2, because you do not need to hand select configuration items. However, environments basically need to be frozen and this totally hinders parallel development. Think about the scenario in which a product owner is making changes to a production system. Or, two people are working at once and make configuration changes. If you use the bulk import/export approach, the full site configuration is affected. One would need to manually cherry pick any parallel changes to ensure configuration is synchronized. All or nothing prevents this unless you freeze or lock down environments or introduce some use of approaches 1 or 2 (with some form of collaboration to identify these changes).

**Approach 4** - This is the most promising due to the ability to easily "see" changes (like you can with diffs, pull requests, etc), but has the biggest technical lift by introducing considerations outside of the Drupal system. Furthermore, there is still the disconnect of two separate Drupal and Git systems. Someone (or something) needs to actually push (synchronize) config into Git when it changes. And, what happens if this configuration changes outside of a developer's sandbox (say, the production system by a non-developer). Furthermore, when should this happen? This seems to suggest or require more advanced tools, DevOps processes, or other items that establish synchronization across environments.

Any of these approaches introduce limitations or require additional technical lift. 

## Composer

Consider me a big fan of Composer. It's a true dependency management system and brings a level of sophistication to the complex relationships between core and contrib. But, most importantly, it's reach is far beyond that of just Drupal. Composer helps connect Drupal to a wealth of external projects and helps managed supported versions.

I was thrilled to see Drupal finally adopt Composer as part of its ecosystem. It's in core. It's widely adopted in contrib. But, there are challenges. 8.1 was the first version of Drupal to officially announce use of Composer, long after many sites began to establish best practices and learn the differences found in the 8.0 release. If anything, this should have happened long before the 8.0 release.

The release of 8.1 unlocks entirely new considerations with Composer. Existing tools like Composer Manager became deprecated. Many contrib modules already leveraged or defined composer.json files for compatibility with the *drupal-projects* Composer namespace. As such, entirely new development workflows become possible. Composer-based workflows, similar to Drush Make, allow specification of core, patches, contrib projects, themes, and libraries to all be managed from Composer. This management workflow deprecates many features of Drush - including commands for executing make files and downloading modules.

You can't knock innovation (three cheers for this progress, folks). You can knock the additional lift it's going to take folks to become comfortable with this. You can knock the fact that we now support multiple approaches and tools (flexibility yields too many degrees of freedom). With sophistication can come frustration and now deeper learning curves. I've already been fighting this. Composer workflows lack maturity because the community has yet to define the best practices. A lot of Composer workflows are fraught with version incompatibilities, yet another tool with new commands, and a lack of understanding on how a series of Composer files all come together from Drupal core, contrib, etc.  

## Impact

I find we often promote innovation over considerations of the technical lift. I wonder what impact this has on people, as Drupal 8.0 was a huge step forward already, but innovation now happens with every dot release. I have to wonder if we're raising the barrier of entry to Drupal, not lowering it. Is Drupal 8 only for enterprises that can afford robust DevOps rich infrastructures and highly trained developers? The developer experience has been widely praised -- and it should be. It's fantastic. The technical lift was already high for Drupal 8; but now the required learning will continue with every dot release. I praise a lack of stagnation (fully recognizing the long development cycles of each major version of Drupal), but that which will continue to make Drupal stronger also serves as a drawback. Defining best practices and maturing the technology takes time in an open source community, as does the learning of it's members. We need more experts and this requires stability to ensure experts can be born.

The broader community needs the opportunity to keep up. Community members develop the documentation, contributed modules, themes, support, and so much more. Many build sites that use Drupal, establish the DevOps tools, workflows, and infrastructure that often complement Drupal-based solutions. In lieu of additional enhancements in the next dot release, maybe we should consider stabilization. I can't help but wonder where the balance is between innovation, modernization, and the technical lift in learning this new system. My hope is we continue to see a vibrant community that adopts this innovation with vigor and a passion for open problem solving. As, this is just what we need to establish maturity, thought leadership, and the definition of best practices to build polished solutions. 

We're standing on the shoulders of giants, but we need more giants. We need more diversity of opinion to become stronger. We need more leaders born from experience. How does this adoption happen without giving the broader community a chance to catch up?