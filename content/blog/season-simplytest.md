---
title: "The Season of SimplyTest"
date: 2019-01-18
slug: "season-simplytest"
tags: ["development", "drupal", "people"]
description: "A transparent look at where SimplyTest.me stands, what progress was made in 2018, and what the roadmap looks like going forward."
draft: false
---

Last year was spent primarily learning about SimplyTest. We did make some progress, but I think “keeping the lights on” for a system of this complexity was quite a feat after the project transfer. It’s a unique and fairly complex endeavor that bridges all elements of an open source project, a completely free service, and underlying infrastructure. I see all of the good and the bad that comes from each aspect: system maintenance, feedback from community members, customer service (Slack, Twitter, etc), system outages, and more. I recognize how valuable this service is to the community and I strive to offer the best service possible.

I serve as the SimplyTest lead. I do most things and do not have a team. I steer both the current system (primarily for stability) and maintain the vision to help modernize, simplify, and scale SimplyTest with time. I balance my time by prioritizing impact, knowing I work full time and have a family. There are times progress stalls given time constraints and this seems to mirror much of the concerns people raise around a perceived “stagnant” system.

There isn’t vibrant additional contribution to any aspect of SimplyTest. But, I do want to recognize and thank Greg Boggs for his help, especially with system administration. Iris Ibekwe, who developed a new Drupal 8 theme for our future front-end. Several members of my team (Jonathan Daggerhart, Ryan Bateman) at Hook 42 have helped start build out aspects of the Drupal 8 front-end with me. I welcome help and also need to do a better job of asking for it.

There are little to no finances tied to SimplyTest. We are fortunate to have server-level sponsors (shout out to Maloon, Druid, and Linode), but we must make use of free services/tools, pay personally out of pocket, or (very recently) get reimbursed through donations. All labor has been volunteered and some sponsored by Hook 42 (thank you so much!!). I personally have paid for a new design and logo, stickers, domains, and more, long before the Open Collective was established.

At the end of the year, I often take time to work on outside things (e.g. professional development or community work). 2018 was no exception. I had a full backlog of items I wanted to tackle with SimplyTest and wanted to share the last two months of progress.

# Development server

Given the underlying complexity of the various distributed systems involved, it is incredibly hard for people to set things up on their own. This hurts contribution.

Thanks to a generous donation from Linode, we received credit on their platform for new infrastructure. This allowed us to set up both a front-end server and a worker server to be used for development. While this is quite close to being finished, this is a huge milestone for SimplyTest to ensure we vet changes on non-production systems and foster an environment that is safe to make changes such that others can learn the system to contribute.

# Clean up procedures

The setup of the new development servers required snapshots and images of the underlying infrastructure containers. Just the action of creating these caused the system to go down due to a lack of storage. This uncovered an underlying issue where spawned instances were not being properly cleaned out and the subsequent images were massive.

Processes were developed to manually clean these out. Based on an increase in usage, the system subsequently went down several other times. This was then scripted and moved into daily cron. We are actively monitoring the disk utilization to ensure these processes hold and stabilize the system.

# Continuous integration

A brand new Jenkins server was set up to afford opportunities to automate tasks in and between servers. Attempts were made to automate the creation of the development servers. But, there were many complications encountered, like the previous wildcard certificate used for the instances that was not scripted through LetsEncrypt. The storage issues ultimately prevented the automation from moving forward and the amount of technical complexity to make this a reality with the current system is likely not worth pursuing a complete solution. However, it’s nice to have this tool in place to move forward and maintain a platform for learning and rolling in automated improvements.

# New SSL for the web frontend

During the creation of the development servers, the scripts leveraged to generate SSL certificates through LetsEncrypt were executed on the development servers multiple times due to both networking issues and updated configuration. Cleanup was required to remove some failed past attempts on the production system tied to certificate renewal. All of this work required the LetsEncrypt service to be invoked multiple times in a development-only capacity.

Sadly, this effort caused us to hit the LetsEncrypt rate limit. Within a few days, the SimplyTest.me SSL certificate expired (at the most inopportune of times). While it required funding, this ended up being an opportunity for us to purchase and place a more permanent SSL certificate to minimize maintenance moving forward (LetsEncrypt has quarterly certificates). This was our first use of the expense system in our Open Collective to reconcile and publicly share the expense.

# Monitoring

Given the expansion of infrastructure, it’s imperative to have monitoring in place. As a start, we’re leveraging the free offering of Uptime Robot, which now covers outages for all production, development, and CI infrastructure. There are opportunities over time to expand this for storage thresholds, proactive SSL certificate notifications, SSL expirations, and more.

# Expanded donations

We’ve not done a great job of marketing our Open Collective because I believe firmly that people need to be informed of where SimplyTest is heading and can recognize what incentives come with their donations (aside from the service running).

There is a lot of strategy involved and many ideas I wish to explore in the coming and future years (e.g. infrastructure for a modernized system and a paid internship to help those underrepresented in tech). However, several people in the Drupal community and the Drupal Association, has joined as backers. I can’t thank you all enough. I welcome others to join as backers and will work to outline these opportunities and vision moving forward.

# Conclusion

I’ll continue to invest my time to make SimplyTest the best it can be. It’s a labor of love but one of the most rewarding and unique contributions we have in our community. I couldn’t be more confident in where this is heading and look forward to many vibrant years ahead for the service.