---
title: "SimplyTest.me Roadmap (Early 2018)"
date: 2018-02-21
slug: "simplytestme-roadmap-early-2018"
tags: ["drupal"]
description: "The purpose of this blog post is two fold:   1. To be clear on what and how we plan to address issues with the current system.  2."
draft: false
---

The purpose of this blog post is two fold:   1. To be clear on what and how we plan to address issues with the current system.  2. To address where the service is going.The service has a bright and promising future ahead as an open source platform that will serve people well and give people a chance to learn through contribution. The service will remain free and will be community sponsored.

 

Before I begin, I want to start with an acknowledgement. I’m totally in awe over how far ahead of it’s time the SimplyTest service was and this is a testament to PatrickD’s efforts throughout the years. As an example, the service is based on LXC, which appears to be the precursor to technology like Docker. Patrick also created an entire library of DevOps scripts that was created and running well before DevOps was mainstream. All this time, the community was benefiting from a really cool and innovative product. The goal is for the tool to get back to that same level of prominence with the upcoming work.

 

Thanks to several members of the community, there is some further clarity on the longer-term objectives. And, community members have been reporting several issues. I hope this blog post communicates how we plan to address “all the things.” Special thanks to Greg Boggs, as he has been helping ensure both the current SimplyTest.me service has been evolving and has been instrumental in helping define a vision for the future. His systems administration help is vital, as my expertise primarily resides in the development/DevOps space.

# Short Term

By today's standards, we have some work to do to maintain the service. Based on the complexity of the current build and my current knowledge of things, we’re going to try to minimize what we need to do to keep the service running and try to invest efforts into modernizing the service. This will help us deliver a better service. We will prioritize significant service degradation and de-prioritize new feature requests.The following issues are what is needed to “keep the lights on.”

 

- Improve logging and debugging: Right now, it’s rather difficult to debug issues when they arise. This situation is making it nearly impossible to resolve issues quickly. We will be updating the error logging of instances so we can more easily triage problems. We also see a real opportunity to expose errors to end-users, as this can be helpful for debugging (especially for patches). [Issue](https://www.drupal.org/project/simplytest/issues/2946735)

- Finish upgrading to PHP 7: Both Drupal 8 and Composer require PHP 7. The latest versions of Drupal 8 would not even provision on the service, so we needed to perform the upgrade. As we’re new to the maintenance of the server, we’re still sorting out if this was done properly and completely. [Issue](https://www.drupal.org/project/simplytest/issues/2942862#comment-12471747)

- Fix distributions: Right now, distributions are broken. We need the first two issues to get resolved before we address this. Based on timing, our PHP upgrade likely caused this and we’ll explore necessary PHP extensions and/or configuration. [Issue](https://www.drupal.org/project/simplytest/issues/2907510)

# Near Term

Efforts are needed for the product to be simplified, modernized, and will get us to a point we have a new beta release of the service. The current service will remain fully intact until the new service has been fully released. All items listed below are open for contribution.

 

- A new ReactJS based frontend: The data in the SimplyTest.me interface is both manually and automatically synchronized from web services sponsored from Drupal.org and copied into the SimplyTest Drupal application. This overhead is no longer needed and data should be dynamically pulled and rendered using a modern JavaScript framework. In line with where the Drupal community seems to be going, the current interface will be replaced with a React-based frontend. Work has begun on this. [Issue](https://www.drupal.org/project/simplytest/issues/2939866)

- A new provisioning platform: The current LXC-based system seems to work well for one server. Complexity is added to control and load balance across multiple servers. To resolve this, many people have recommended both cloud-based technology and Docker containers. Work has started on a new Docker image that accounts for the configuration and parameters specific to SimplyTest. [Issue](https://www.drupal.org/project/simplytest/issues/2939497)

- A new hosting platform: Currently, SimplyTest runs on sponsored bare metal servers. Without a significant investment in both Kubernetes and monitoring tools, sharing load across bare metal servers would introduce complexity that doesn’t exist in a cloud-based hosting provider. As cost is a significant factor, we’ve looked at Digital Ocean droplets as a way to lower the cost per instance, have support for Docker, and get a web service driven API for instance management. A new sandbox module for Digital Ocean’s API was created. [Issue](https://www.drupal.org/project/simplytest/issues/2939497)

- A new DevOps system: An upgrade to Drupal 8 has been long planned for SimplyTest.me. A new Drupal 8 site will be set up that incorporates the new React interface and manages instances by calling the Digital Ocean APIs directly. This system will manage instanced by controlling the provisioning, the teardown, and the operational logic of the system. [Issue 1](https://www.drupal.org/project/simplytest/issues/2939866), [Issue 2](https://www.drupal.org/project/simplytest/issues/2939497)

- A new design: It’s time for a bit of a facelift for both the visuals and the user experience. I’m going to be mocking up the new interface as a wireframe, solicit feedback, and get a new logo and design created for the application. This will then be incorporated into the distribution as the theme, which may include enhancements to the React application. [Issue](https://www.drupal.org/project/simplytest/issues/2946735)

# Long Term

Before being able to implement the new system, there certain things need to be in place.

 

- Set up a non-profit entity: This service has not been set up to make anyone money. It was set up to be a free service that benefitted community members. It will stay that way, but these new strategies will incur costs that make the conventional server sponsorship obsolete. Setting up a non-profit creates an entity that is inline with this intent. We can manage expenditures, receive donations, and operate in a transparent and legal-friendly manner. A brief discussion was held with members of the DA on Slack, but it was clear the DA is moving away from being a financial support entity for community-led efforts. So, establishing a non-profit seems to be the right move.

- Set up Stripe and donations: The Drupal 8 infrastructure will need to be set up that allows for donations. Based on cost, I plan to leverage Stripe and have already been consulting with Matt Glaman of the Drupal Commerce team. This adds yet another service to pay for, but I expect to receive non-profit rates and may individually sponsor these fees should they not be overwhelming.

- Get sponsors: Before we release the new system, which will spawn many Digital Ocean droplets per day, we need recurring sponsors. I also intend to collect individual, one-time donations and donations from any camps or conferences holding sprints. Recurring sponsors will have access to all expenditures and will be able to see summarized information from other sponsors. Ideas are being discussed about sponsor-level benefits. Currently, logos are on the site and displayed during instance provisioning. I welcome ideas on how we can ensure this is an attractive opportunity for sponsors, outside of the general goodwill.

- Clean up the issue queue: The issue queue has a lot of legacy issues. Once this is all said and done, we will groom the issue queue.

 

If anyone has any input on this roadmap, please feel free to connect with us on Twitter or in the issue queue.