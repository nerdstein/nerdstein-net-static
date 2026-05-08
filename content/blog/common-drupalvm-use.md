---
title: "Common DrupalVM Use"
date: 2016-02-29
slug: "common-drupalvm-use"
tags: ["development", "drupal"]
description: "I long struggled with how to effectively do local development in Drupal."
draft: false
---

I long struggled with how to effectively do local development in Drupal. Few would argue the merits of doing local development over working directly on a production system. While the problem seems straightforward, nothing seemed to work quite right. It took me quite a while to land on DrupalVM. 

I'd like to explain how I landed here and some of the ways I use/configure DrupalVM to support my needs.

 

## Requirements

This whole experiment made me think about what criteria I was evaluating these against...

- ***MOST IMPORTANT*** - I really want my solution to **JUST WORK** with as little set up as possible. Most tools I have tried have some inherent limitation, which forces me to do advanced or additional setup.

- **Virtual Machine** - Development tools and setups are never the same across projects, so I want to **avoid installing tools on my local system** that may force me to tune and/or change when switching between projects. This is a major time dump and one that seems to be a significant waste.

- **Performance Friendly** - When I create my local set up, I do not want a resource-starved setup. It pains me when you initially load the site and cannot even get the page to load. I don't want to do any additional, manual configuration it to get it to perform well.

- **Destructable** - I want the full discretion to destroy and rebuild my local environment at will. Especially if I am working on a project in which the environment is regularly changing or evolving.

- **Configurable** - No solution should make assumptions about the needs of the project. I could use any version of Drupal, Drush/Drupal Console, PHP, SOLR, MySQL, or even the distribution or version of Linux. I may have specific tools I want installed for one project I might not want for another. I don't want just the ability to go in and manually configure, because VM may be blown away at any point. **The configuration needs to be persistent** to support rapid provisioning.

- **Robust and Unassuming Toolset** - None of my clients use the same tools, especially when attempting to mimic production environments and their tools. There are so many different factors: Git, SSH, Drush, Drupal Console, SOLR/Search Backend, Varnish, Memcache, Frontend tools (Ruby/Gems, Node/NPM), Composer, etc. I want the ability to rapidly use and configure the tools I need without this being an encumbering task. And, ideally, this is configuration that is persistent and can be shared across development teams.

- **Unassuming development workflow** - Every team and project has adopted their own workflow based on team preferences and technical competency. I don't want a tool that only supports workflows defined by hosting platforms, undocumented continuous integration solutions, or poor practices carried over between vendors. I have seen a host of different approaches from make-file driven solutions, repository based workflows, use of SSH/SFTP/SCP, implementations with Drush aliases, etc. I may have preferences, but ideally, my local sandbox can support any or all of these seamlessly.

 

## Previous Attempts

My exploration is not without a comparison and in-depth use of many other tools that could, to a degree, meet these objectives.

- **VDD** - This came up on drupal.org, so I gave it a spin. It's Vagrant-based (virtual machine) and has some nice utility in spinning up a basic LAMP set up with some Drupal-specific tools, like Drush and Git. My biggest issues with this was that it was completely non-performant, it lacked persistent configuration, and lacked robust tools.

- **Various LAMP-based virtual machine images** - Same challenges as VDD but usually lacks the basic Drupal toolkit (Drush, Git, etc). While these can be manually configured or scripted, this adds a level of overhead that makes any generic virtual machine solution cumbersome to use.

- **Acquia Dev Desktop** - This lacked full stack even for their own Acquia Cloud platform, since it's missing Varnish, SOLR, Memcache, and other utilities. It did set up Drush and Git, because Acquia Cloud basically requires it to do anything. It also is not a virtual machine, relying on installing software on your host machine.

- **MAMP and variants** - Same exact architecture as Acquia Dev Desktop but no Drush, no Git, and some assumptions on tools, like PHPMyAdmin.

 

## Why DrupalVM?

This may read like a sales pitch, but I think people need a clear view on why it stands out from the crowd.

- DrupalVM leverages well-adopted virtual machine technologies in Vagrant and Ansible for an elegant architecture. Vagrant helps manage VM-related operations (like provisioning) on top of your host machine VM hypervisor. Ansible is a popular system automation framework with an open-source library of available resources. The combination is hands-off virtual machine orchestration.

- DrupalVM creatively establishes a modular architecture with it's various Ansible roles. Each role is maintained independently and has it's own separate configuration options and is maintained.

- DrupalVM's configuration is persistent and robust. DrupalVM aggregates the specific configuration in the Ansible roles into one persistent file. This includes practically everything from system and software versions, Composer/Node/Ruby tools, sync'd local drives (NFS mounts), and much more. This means teams can work off of the same local specification closely aligned with production environments with little surprise.

- DrupalVM's configuration requires little out-of-the-box changes to get a working and have a relevant VM set up for typical use cases. It also provides several example configurations for a variety of hosting platforms and common use cases.

- It works and is performance-friendly out of the box. For serious (insert Zoolander face here).

- It's an evolving tool and actively maintained. The author, Jeff Geerling (Geerlingguy) responds in a timely fashion to both help requests and potential issues. It continues to evolve through community use and thoughtful discussion.

- The balance between the robust toolset, sync'd drives, and configuration layer make it desirable for practically any use case I've run into. It is not prescriptive whatsoever.

 

## Basic Workflow

**DrupalVM has a quick start tutorial** on drupal-vm.com that summarizes the basics for bootstrapping DrupalVM. I have captured my workflow below, which captures a consistent use of DrupalVM across many projects.

- Locally, I maintain one DrupalVM repository, which I update (git pull) when I start a new project.

- Create a new project directory for your project.

- Inside of the project directory, create subdirectories for *docroot* and *scripts* directory.

- Copy contents of DrupalVM repo (ideally without *.git*, remove it otherwise) into a *box* subdirectory.

- Copy example.config.yml (or another sample configuration file) into a project specific config.yml, configure config.yml for your project settings.

- Add in sync directories for for scripts and the Drupal docroot configuration would be docroot.

- Install the recommended vagrant plugins (host manager and auto-network) and adjust your configuration to support that (e.g. ip_address setting).

- Run *vagrant up* to provision the VM from the *box* directory

- Code ALL THE THINGS!

- When you need to switch, run *vagrant suspend* to pause the VM from the *box* directory

- If you are done with the VM or want to get a fresh build, run *vagrant destroy -f* from the box directory

 

## Learned best practices of using DrupalVM

There are some specific ways I use DrupalVM based on my experience worth sharing.

- DrupalVM default config and make file does not set explicit versions of Drupal and Drush. I've had issues when using the bleeding edge code and recommend these are configured to use stable releases.

- DrupalVM provisioning will automatically set up aliases to the VM on the host machine. I often find myself working on the command line though. To facilitate, I use *vagrant ssh* from the box directory, after a box has been provisioned.

- When you are working off of an existing code base, turn off "build from make file" setting. This will overwrite your docroot.

- Watch out for "install site" configuration when enabled, this blows away settings.php, which may hold configuration for existing code. Back this up locally before installing or do a manual install for an existing code base.

- If your project uses a code repository, turn off "fileMode" in *.git/config* because it will regularly change your *sites/default* permissions: *chmod -R 777 sites/default*

- I usually avoid upgrading DrupalVM within an existing project. There are often config changes between versions of DrupalVM that can be challenging to diff with broader functional changes. I would only upgrade if you need some new feature. Bear in mind, most DrupalVM versions are highly configurable anyways - I would resort to updating configuration and re-provisioning before upgrading DrupalVM.

- If you need to upgrade, don't copy config between projects. Make updates manually and review config changes between versions.

- Use *vagrant-hostupdater *and *vagrant-autonetwork* plugins. These plugins reduce manual steps and potentially harmful configuration around IP-address conflict.

- Don't run multiple machines in parallel, use vagrant to suspend machines, run vagrant up to restore them when needed.

- I use the aforementioned *scripts* subdirectory as a general dumping ground for moving assets between the host and the VM. This is really useful for drush aliases stored on your host, manually downloaded SQL files, or scripts generated on your host you want to run from the VM.

- Bring over project-specific Drush aliases into the VM. This can be incredibly useful to get databases and files from other servers for existing sites.

- Be careful if you wish to version your DrupalVM configuration for a distributed team. Leverage *.gitignore* for the majority of the *box* subdirectory contents excluding config.yml, the make file, and your requirements.txt file. Leave explicit instructions in the project's readme for installing the VM and note any project-specific implementation steps.

 

## Summary

This blog post was a while in the making and likely does not meet everyone's needs. But, this outlines my experience and the considerations I used to come to the solution I am working with today. I hope others find this useful.