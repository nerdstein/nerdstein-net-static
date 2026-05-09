---
title: "Local core development environments"
date: 2017-08-08
slug: "local-core-development-environments"
tags: ["development", "drupal"]
description: "In an earlier blog post, I described my ideal local environment for developing Drupal based projects (DrupalVM)."
draft: false
---

In an earlier blog post, I described my ideal local environment for developing Drupal based projects (DrupalVM). My primary objectives included separation from the host OS, persistence in config (affording disposable sandboxes), and extensibility to customize around project specific configuration (mirroring other environments). In those respects, DrupalVM has spoiled me and I've likely saved hundreds of hours in large part to these efforts (thank you, Jeff and other contributors).

Core development is a different story. Technically speaking, you need Composer, Git, and an environment mirroring Drupal's supported infrastructure (php versions, MySQL, etc). Compared to Drupal based projects, there are far fewer moving parts. There are no contrib modules, no integrated systems (SOLR, as an example), and no complexities introduced by custom themes and frontend frameworks. Equipped with a cloned Core Git repository, I was ready to dive in and wanted a local setup to do so.

Much of these aforementioned considerations make DrupalVM overly complex for this use case. Please note, there is an argument to be made for consistency and familiarity. I made some efforts to poke around with its provisioning configuration to get a working core development sandbox with no luck. I believe I was stuck somewhere between abstraction and composer hell. Also, with the rise of Docker growing in popularity, I decided to try something new.

This introduces me to one of the earlier points I wrote about why I like DrupalVM -- "it just works". I am not a Docker expert but know enough about containers from working at CivicActions to be technically competent and acknowledge the complexities involved. Yet, my expectations are based on my comfort and experience with VMs. A primary measure of success for me is to not have to spend time futzing through something that doesn't "just work" (note: "just work" doesn't include properly configured). I knew I would be near worthless diving into the bowels of Docker based projects (e.g. Docker images and configuration) and was skeptical of contributing back in a technically meaningful way. I also knew that Linux based hosts have far better native support for containers (via LXC) than that of my Mac. Right around this time was the Edge release of Docker For Mac, opening up some new improvements that peaked my interest and saw many blogging about. As such, I decided to spread my efforts around various Docker based projects until I found something that worked for me. I proceeded with both with a sense of skepticism I might need to invest more time debugging DrupalVM and the reality I might need to wait for the technology landscape to stabilize.

I started with Bowline, since this is something my company help maintains. The provisioning of Bowline was superb, I liked its configuration, and the fact it had customizable commands. But, I quickly ran into issues with filesystem synchronization. This was noted as a work in progress by my peers. I was impressed with the integrated proxy system and host management. But, at this point, I decided to move on.

Right at the time, DrupalVM released its very early alpha support for Docker. It was marked as "buyer beware" and explicitly noted as experimental. I wanted to give it a try and was cautiously optimistic I could give Jeff some thoughts on it. After repeated failed attempts to get a functional Drupal environment to load and subsequently filed issues describing the steps I took, I again acknowledged I was out of my depth. It also was not clear to me how the existing DrupalVM based configuration layer interacted with the new docker compose configuration and the subsequent provisioning results. Please note that since my testing, there have been additional releases and, most likely, much more progress and stability I have yet to try.

At this point, I felt I was wasting time that I could actually be working on core and wanted to try to find something as quickly as I could. That day I noticed a tweet about DDEV, which is supported by Rick Manelius and Randy Fay (a very long time Drupal contributor). Installation was a breeze. I was immediately impressed by the fact that it was both a global tool with commands and that it maintained a local, project specific configuration layer. After installing the tool, I ran a few commands and "poof!", a Drupal install! I was a bit surprised but encouraged. I started making some code changes and saw an instantaneous result. I was in business.

After some learning of DDEV commands, and filing some minor issues (e.g. Upping their installed versions of Drush to support something more bleeding edge), I was golden. I was equally as impressed when I stumbled on the DDEV slack channel in Drupal's Slack and was hand held through the challenges I encountered. Due to my novice experience, this was welcomed and I actually felt like I was helping discuss the future of the product (which is still very early in its lifecycle). I expressed that i would like to see a more robust and consistent configuration layer abstracting a plugin-based infrastructure like that of DrupalVM and Ansible. 

The following represents my workflow I used to get a Drupal based sandbox set up for core development with DDEV (command line tasks):

- (one time) install DDEV

- mkdir local-core-project

- git clone --branch 8.4.x [https://git.drupal.org/project/drupal.git](https://git.drupal.org/project/drupal.git) docroot

- cd docroot

- composer install

- cd ../

- ddev start

  Fill out the questions prompted from this command

- When asked for the docroot, enter `docroot`

This is certainly an exciting space right now and I was happy to stumble on the DDEV work. Now that this has been demystified some for me, I am curious to go back and evaluate other active projects. I am excited to check out the progress made by DrupalVM. I have also heard great things about the Docksal project and was made aware of a module-specific Docker environment called Dropwhale useful for maintaining contrib projects and developed by Socketwench. With the current landscape, I'm growing more confident our community is progressing for Docker and local environments in general. Thanks to those who have been right on the cusp of this and contributing solutions for us to leverage.