---
title: "Patterns of DevOps Practices"
date: 2015-11-10
slug: "patterns-devops-practices"
tags: ["development"]
description: "Recently, I read Codifying devops practices, a blog post written by Patrick Debois. This is food for thought."
draft: false
---

Recently, I read [Codifying devops practices](http://www.jedi.be/blog/2012/05/12/codifying-devops-area-practices/), a blog post written by Patrick Debois. This is food for thought. I spent some time trying to identify the patterns I recognize in daily practice. I may continue to update this as I learn more opportunities and categories.

Approached with a *build-measure-learn* philosophy, patterns are less about the "how" and more about opportunities to improve and grow. These opportunities may be considered best practice, but are circumstantial based on your organization, your project, or other factors.

I personally advocate addressing the most glaring problems first, as I've seen that organizations attempt to introduce sweeping change and subsequently fail to introduce even small improvements. Start with low-hanging fruit and get some momentum. Change seems less scary when people can see the fruit it bears. 

## Tools / Environments

- **Build automation** - frameworks/scripts to automate the setup and configuration of environments for consistency (local systems, development/QA environments, production)

- **Development tools** - selection of code-level frameworks and best practices for the frameworks

- **Code repositories** - leveraging code repos for organization, deployments, and restoration

- **CI systems** - centralized on-demand tool to run commands remotely across one or more environments

## Process

- **Release management** - codifying the bridge between deploying code from the repository through the various environments, generating release notes, and automated notifications

- **Ticket workflows** - tickets should follow a defined process that walks through discovery, estimation, development, QA, and sign-off; dashboards should provide just-in-time views of status

- **Communication synchronization** - most people use chat-related tools so integrating systems and updates into the chat service helps inform teams of progress, like when code is submitted for review, when it's been reviewed, etc

## Mediation / Enforcement

- **Code review** (automated or manual) - the perfect opportunity to catch mistakes and hold teaching moments, rolled up into documentation of best practices on how to perform a code review

- **Smoke testing** - peer testing before a code is merged into the code base or before deployment

- **Automated testing** - 1 - identify **what** you want to test (major features, visual issues - "everything" may not be feasible), 2 - identify **what** existing tools exist, 3 - identify **when** tests may run (a targeted test may run more frequently than a full regression test)

- **Development processes** - all tickets should have specific criteria to ensure development and hands-offs are smooth

## Feedback / Learning

- **Retrospectives **- ask teams and what problems they face, aggregate these into the problems you wish to solve; repeat with clients and other stakeholders; define trends and identify the priorities; identify potential tools or options to solve the prioritized issues

- **Architecture documentation** - teams need a "big picture" view on what a project is, the goals/objectives and how a project has been built; this can include expected development standards

## Measurement / Auditing

- **Log Auditing** - manually or automating the auditing of logs identify development improvements or design flaws

- **Notifications** - server level tools that monitor activity and performance of servers and environments proactively (both for security and preventative measures before a server were to go down)

- **Development metrics** - ticket-level reporting on estimates versus actual hours, tracked against well-known milestones (MVP, launch, phase 2, etc)