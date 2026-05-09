---
title: "A brief comparison of text editors"
date: 2013-01-01
slug: "a-brief-comparison-of-text-editors"
tags: ["development", "drupal"]
description: "A comparison of text editors — from Dreamweaver to Espresso to PHPStorm — and why the right tool changes as your workflow does."
draft: false
---

To innovate, you often have to risk getting out of your comfort zone. The last several years, I have had varied needs which have required me to evaluate new text editors that offer more robust functionality.

For years, I used ***Dreamweaver*** primarily as a text editor. I never used (or liked) the fancy GUI HTML editing. But, Dreamweaver provided three primary features that I loved. The syntax highlighting for PHP / JS / HTML really worked for me. The code could be split up into different Dreamweaver projects (with some directory as the project root). And, it has an integrated FTP manager to push files between a local server and a remote one. The downside is that the text editor did not scale well for me.

As I grew, I began asking different questions and faced new challenges. What happens if the server crashes? What happens if I want to revert my code back to a previous build? Furthermore, I had sites get compromised because of using FTP and knew there were better solutions out there. To grow, I leveraged SSH, version control systems with tagged releases, local development on my own machine, and the command line. This afforded me better opportunities to use system-level tools like grep.

My new focus actually limited my reliance on the features of the text editor. Dreamweaver started to be bundled in with the Creative Suite and the price really started to hike. And, I wasn't using the majority of Dreamweaver's features intended for less technical folks interested in automating lower-level details. The tool has a lot of polish, but no longer met my needs. I wanted the tool with the most usability. I focused on organization by projects and providing the best syntax highlighting possible. This led me to ***Espresso***.

Although it never received a wild amount of press, Espresso clearly was implemented with usability in mind. The design of the tool is clean. The featureset is paired back and straight forward. It split up code project to project (and allowed simultaneous projects open in different windows). And, the syntax highlighting really integrated well with PHP. This allowed me to do programming in Espresso and version the code in the command line.

Over time, I started running into limitations. Espresso, while very clean, had issues with formatting code (and a lack of options to configure this in the way I wanted) and it did not allow me to specify custom file extensions I wanted it to parse without creating a custom Sugar. On many blogs that I read, many text editors were offering features for automated testing frameworks, version control integration, and even coding standards, on top of a robust/configurable text editing featureset. Tools like NetBeans, PHPStorm, and Sublime Text have a growing community, a vast set of plugins, and solid documentation (wikis, blogs, etc). Once my development workflow stabilized, I came back full circle.

I have recently adopted ***PHPStorm***, which cleanly integrates with GIT, Drupal development standards (coder with PHPCS), and XDebug for testing/debugging. It has a learning curve, since it has a vast amount of ways it can be configured. It allowed me to add file extensions like module, inc, install, which is commonly found in Drupal modules. It has contextual recognition of Drupal's hook system. It even has integration with Drush from within the tool itself. These features then limited my need to go to the command line to perform common operations. The drawback is that I am not sure how well this tool would integrate with other platforms outside of Drupal. My guess is that due to the extensible configuration and integration, it could be configured to work well with other platforms if plugins did not already exist.

I can't speak to your personal needs. But, don't hesitate to think outside of the box. Stepping outside of your comfort zone may afford opportunities.