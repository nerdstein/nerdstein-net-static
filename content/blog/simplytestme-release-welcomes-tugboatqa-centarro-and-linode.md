---
title: "SimplyTest.me release welcomes TugboatQA, Centarro, and Linode"
date: 2019-10-06
slug: "simplytestme-release-welcomes-tugboatqa-centarro-and-linode"
tags: ["development", "drupal"]
description: "On the evening of September 13th, SimplyTest.me launched a major new release of the product."
draft: false
---

On the evening of September 13th, [SimplyTest.me](https://simplytest.me) launched a major new release of the product. The product release achieved three major goals:

- Replacement of the backend with TugboatQA

- A new one-click demo framework

- A new development environment

All efforts could not have been possible without the generous sponsorship from [TugboatQA](https://tugboat.qa) (a product created by [Lullabot](https://www.lullabot.com)), [Centarro](https://www.centarro.io), and [Linode](https://www.linode.com). And, community time offered from [Hook 42](https://www.hook42.com).

The rest of this post outlines the release and its significance.

## TugboatQA Backend

### How did we get here?

The backend infrastructure of SimplyTest.me was one server running as a single point of failure. A bulky, monolithic server running a LAMP stack and concurrent virtual hosts/databases/etc. The system had no viable backup, no load balanced failovers (a money problem, not a technical problem), and no affordable replacement.

Community conversations were held [to advise on an open source replacement](https://www.drupal.org/project/simplytest/issues/2939497). Many agreed on a panacea that included the use of Docker and Kubernetes running on a cloud-based provider. This gave end users cleanly isolated instances and an infrastructure capable of rapidly provisioning and terminating instances through well-adopted, right fit technologies. This could have been an impactful contribution back to Drupal, too.

While this approach would have been great, who would pay for it? Rough numbers showed that even with the use of tiny spot instances through AWS, we still would have paid at least a few thousand dollars a month for our free-to-use service. Significantly more during major events, like DrupalCon and camps. And, no money or sponsorship to change course. Furthermore, we would have needed to do a ton of technical work across the full stack to achieve this goal. Since the current site still needed to be maintained, this approach would have certainly been a challenge.

Fears had been growing around the sustainability and maintainability of our underlying infrastructure. The backend system repeatedly would go down and over a decade of technical debt had built up. The divergence of Drush 8 and 9 and support for past versions of Drupal also complicated things. The issues were becoming more and more complex. I needed to solicit the help of experts like [Elijah Lynn](https://www.drupal.org/u/elijah-lynn) and [Greg Boggs](https://www.drupal.org/u/greg-boggs), while trying to respect their available time.

Matt Westgate and I connected at [DrupalCamp NJ](https://www.drupalcampnj.org) 2019. In 2018, he introduced me to TugboatQA. But, at the time, the lack of an API held back any integration possible with SimplyTest.me. That changed by 2019 as the product matured. This was welcomed news, but I maintained a degree of skepticism that a QA-based DevOps tool could be leveraged for the full set of needs. I maintain the opinion that SimplyTest is more difficult than people initially acknowledge, regardless of people’s good intentions to make suggestions or offer advice.

When we revisited our conversation, SimplyTest.me just opened our [OpenCollective](https://opencollective.com/simplytestme) but still had very little funding raised. I had a lot of technical questions for the Tugboat team around features and we discussed their high-level approach to achieve my goals. It seemed possible. We exchanged some high level statistics on usage and I finally asked how much it would cost. Their team graciously agreed to pay for our backend. Game changer.

While we had a long road to build out this replacement, the generosity of both Lullabot and TugboatQA to pay for the backend solved a huge hurdle and may have saved the future of SimplyTest.me. It ended up meeting our goals for a new backend. Concerns were raised from the community about not using an open source service/product. This type of situation raises awareness around the harsh realities people like me face when trying to sustain open source communities and run a service with limited fundraising, mostly volunteer led efforts, and minimal corporate backing. I’ll blog about this topic later, but both [Dries](https://dri.es/balancing-makers-and-takers-to-scale-and-sustain-open-source) and [Lullabot](https://www.lullabot.com/articles/healthy-open-source-maintenance) wrote excellent articles about related topics.

### How did we approach this?

The best engineered solutions are ones that are iterated through what is learned. We made two major architectural passes to iron out design decisions.

TugboatQA is based on the concepts of previews. Previews are created from branches on repositories, where new code in the repository could be deployed on a preview for quality assurance. Previews are configured by a set of scripts defined in a YAML file on that branch, similar to a Docker Compose file. SimplyTest.me instances get code from external repositories specific to what a user selects. If SimplyTest were to use a repository, it could only leverage the YAML configuration since the code would be pulled elsewhere.

We started with this approach to create previews from branches. SimplyTest.me, still running Drupal 7, leveraged PHPTemplate to create dynamic preview definitions in YAML. The YAML would change based on what SimplyTest users selected to test. Definitions could clone Drupal, select a version, pull down projects, load patches, and perform installations. This generated YAML was pushed to a unique branch in a repository, where each branch represents the desired submission. All git related details were made configurable and leveraged a Github-based PHP project to properly respect environments and not push code with credentials. Once the branch existed, the Tugboat API was invoked to create the preview through Tugboat’s downloadable CLI tool. I personally ported a Backdrop TugboatQA module into Drupal 7 and posted it [on Drupal.org](https://www.drupal.org/project/tugboat) for others to benefit from. This module is a simple utility and abstraction for access tokens, logging, and invoking Tugboat commands uniformly.

After the first pass at the architecture, the process was generally working. We had scaffolding for Drupal 7 and 8, projects, patches, distributions, and installation logic. The primary issue was performance. It took a lot of time to create each preview. Each provision performed similar, preliminary steps: it created the containers for the infrastructure, loaded things like PHP-APC and PHP extensions, cloned Drupal, installed Drush, etc. TugboatQA had already solved this in their platform with a feature called Base Previews. In short, there are one or more branches that held the YAML definition of cached previews. SimplyTest was able to extract common scripts for Drupal 7 and 8, copy base previews, and apply the preview-specific configuration in the preview’s own specific branch. This sped things up significantly.

[AmyJune Hineline](https://www.drupal.org/u/volkswagenchick) led testing efforts to make sure we maintained feature parity from the old to the new backend. We iterated and worked through a defined set of feature-based issues that she created until we stabilized the new system. This methodical approach to testing with a set of issues tied to features will help us when we look to launch Drupal 8 in the not-too-distant future.

While we still have some known gaps causing failures, like executing make files for Drupal 7 distributions, we were comfortable launching the new backend and remediating issues as they arise.

### Key Outcomes

This new backend has already had significant impact on the project and the service offered to users.

- Radically simplified systems

- Removal of the old backend server

- Removal of HAProxy logic

- Removal of backend SSL certificate

- Empowered the SimplyTest web application to define and control previews created

- Drastically reduced the amount of supporting code that built up over years

- Removal of legacy bash scripts that were retrofitted for newer versions of Drupal

- Replaced the custom web application to backend interaction with a cleaner, decoupled approach: shared repository and web service API

- Offered users drastically better stability

- Removal of maintaining highly customized legacy servers that were difficult to maintain/update with updated technologies and changes potentially impacted the entire service, not just specific instances

- Isolating failures to either service provider outages and/or gaps in the SimplyTest application, not a bespoke, highly customized backend server

- Rapid changes are now possible

- New instances are not tightly coupled to other running instances

- Simplification opens up new opportunities for contributors to participate without having the concern of bespoke infrastructure setup.

### Acknowledgments

I want to thank TugboatQA ([Matt](https://www.drupal.org/u/matt-westgate), [James](https://www.drupal.org/u/q0rban), [Ben](https://www.drupal.org/u/blc)), Jonathan Daggerhart ([daggerhart](https://www.drupal.org/u/blc)), AmyJune Hineline ([volkswagenchick](https://www.drupal.org/u/volkswagenchick)), and [Hook 42](https://www.hook42.com) (giving me contribution time and sending me to camps that I used to do this work and collaborate/sprint on this effort).

## One Click Demos

### How did we get here?

Drupal distributions have been a significant issue for SimplyTest. Drupal 7 had stronger opinions on distributions, primarily around the use of specifically-named make files. Drush enabled scripting covered most of the use cases to build distributions programmatically. But, loose dependency definition and inconsistent use of standards still caused many issues -- many of which community members looked to me to help triage and support after SimplyTest would fail to create instances due to issues that were introduced.

Drupal 8 still feels like the wild west for consistencies between distributions, primarily caused by how core initially adopted Composer (which is evolving and may be worth revisiting for impact to distributions). A simple comparison between popular distributions like Lightning, Commerce, and Contenta demonstrates my point. Each distribution would likely require custom considerations for SimplyTest to work properly.

[Ryan Szrama](https://www.drupal.org/u/rszrama) approached me to see if SimplyTest could be used to serve as the demo framework for [Drupal Commerce](https://drupalcommerce.org) (specifically, the Belgrade demo). This presented an opportunity to improve SimplyTest, raise funds, and explore paid contributions (which was a goal of mine outlined during the vision/roadmap presented at[Drupal Camp Asheville](https://www.drupalasheville.com) 2018). Ryan agreed to sponsor both the underlying architectural changes to enhance SimplyTest and the specific implementation for Drupal Commerce.

Side note: it is inspiring to see how Ryan has established a sustainable business primarily around an open source product that routinely gives back to Drupal. Centarro continues to find creative ways to give back even more.

### How did we approach this?

While our primary goal was to launch a one-click demo feature for Drupal Commerce, SimplyTest is a tool that serves all people and it would have been a wasted opportunity to not build in the capability for additional one click demos. We leveraged a custom hook to allow submodules to register a one click demo. This behaves similarly to the plugin system in Drupal 8. Submodules then invoke the hook, which references a YAML definition. It is expected that the definition supports other SimplyTest features for patches, loading of other projects, and more. Base previews still need to be defined manually and managed through the repository, for now. SimplyTest then loads the registered one click demos and displays each as a button through the web UI.

We shipped this release with support for both Drupal Commerce and the Umami demo. We welcome others interested.

### Key Outcomes

- Created a new feature that made the creation of Drupal-based demos with one click

- Created an extensible framework that solved a long-term difficult issue with distributions and allowed other distributions to be easily rolled in

### Governance

I still have not fully established guidelines to help with the governance of this new feature. I believe it’s important for businesses that sponsor SimplyTest to be eligible for their open source distribution to be delivered as a “one click demo”. However, completely open source demos, like Umami, should be eligible too. Fundamentally, I believe it’s important to focus on widely adopted cases around Drupal 8. Maintaining every distribution across every version of Drupal seems like a challenge for this approach. While there will be some discretion, I promise to work with the community in good faith to roll this out for future potential needs.

## Development Environment

Given the fact that we were making a significant change, we were able to revisit the creation of a development server from [my last attempts over new years](https://nerdstein.net/blog/season-simplytest) (TL;DR - way too difficult). In many ways, the new backend simplified the overall systems. A new dev server was imperative for our testing efforts to launch the new backend. The legacy backend server represented the most complex part of setting up a development environment. And, this was now going away. This made the task a lot more simple to accomplish.

Linode offered SimplyTest sponsorship money to use their infrastructure. We were able to leverage these funds to run a Linode for the web front-end during the entire time we were developing the integration for the new backend. A very basic LAMP stack was created and the Drupal database and files were cloned from the production Drupal application. This unblocked the involvement of others to help test and prepare for the new release.

I thank Linode for giving us this assistance and I continue to support them in other endeavors. We requested and just received additional funding for continued support of the development infrastructure.

## Conclusion

When I transitioned to lead the project, I knew I had challenges ahead of me. I knew the backend needed modernization. I knew I wanted more people and companies to help participate in the sustainability of the system. I knew we would need funding to open up future opportunities. I had ideas but no clear path to move it forward. I invested as much time as was needed to get to this day and it wasn’t even possible without the help of others and the new, generous support of TugboatQA, Centarro, and Linode combined with contributed time from Hook 42. I’m glad we got here. The work is not done. But, I feel much better about where this is heading now that we have this major milestone behind us. I also continue to be grateful for the largely volunteer-led efforts from community members that helped in all capacities.