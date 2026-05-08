---
title: "SimplyTest.me From The Ground Up"
date: 2021-09-22
slug: "simplytest-from-ground-up"
tags: ["development", "drupal", "people"]
description: "When I took over as the project lead for SimplyTest."
draft: false
---

When I took over as the project lead for SimplyTest.me, the previous lead shared three primary things with me:

- The system had a non-trivial amount of technical debt and was rising more with time

- Significant changes were coming with Drupal 8, Composer, Drush, and more

- His interest was elsewhere

As part of my proposal, I promised to do what I could to revitalize this. While this effort has taken years, we have hit another major milestone in our journey: 

**We launched a completely new version of SimplyTest.me.** We rebuilt the system from the ground up in an effort to revitalize the project. It’s time to tell the story.

# The Old System

Architecturally, the SimplyTest I inherited had three basic systems: the web server front-end, the worker server backend, and a proxying system that glued everything together. Everything was manually maintained and largely custom. 

- The servers were hand-built and required a ton of maintenance. All of the scripts to run the system were custom.

- The worker backend was a glorified, monolithic LAMP stack that would provision and deprovision virtual hosts, databases, and hostnames on the fly.

- Cleanup routines would fail commonly on system updates, disks would fill, logs wouldn’t rotate, and the maintenance burden was high.

- Major upgrades to components or the operating system would have caused an indeterminate amount of breakage. If you tried to fix and subsequently broke any part of the system, this would impact all of the running instances.

- And, there was no failover or load balancing.

- The application was running on Drupal 7, which means it was almost three major versions behind.

- Backups did not readily exist.

SimplyTest did not have an infrastructure that afforded easy development or encouraged contribution from others in a safe and straight-forward way (without basically using the fragile production systems). Making changes often broke things and the systems would go down routinely. It was not good.

People would complain. A lot. We tried to keep up. But, the service wasn’t stable, nor was it easy to keep up with the latest innovations our community was developing. People routinely let me know about it. They also would routinely blame SimplyTest for issues with their own projects by expecting me, the maintainer of the service, to debug their issues. I recall a vocal community member persistently accusing the system of being broken because “it works on their local system” only for us to find one of the dependent third-party assets had a broken link in their module’s library file (which they already had downloaded locally and they didn’t properly test it). 

It was an incredible effort to just keep the lights on. And, it wasn’t sustainable. It was important that we created a new future.

# Rebuilding SimplyTest

While a fresh approach was desperately needed, we have finally reached a point where SimplyTest.me has been rebuilt from the ground up. We spared no opportunity to modernize the project, which allowed us to shift our attention back to serving the community. The following sections highlight our accomplishments around revamping SimplyTest.

## Goals

Revitalizing the project needed to be prioritized around what our users would get value from. As an example, lowering technical maintenance or eliminating technical debt affords more time to develop the features of SimplyTest.me or more quickly introduce changes tied to new community innovation (see: Gitlab workflows in drupal.org, updated PHP version support in Core, Composer/Drush improvements, and more). Time spent working on the system would not go toward keeping the lights on, but actual value built into the project our users would benefit from.

Increasing contribution and available contributors is a long-standing goal. Not only do I want SimplyTest to be used for lowering the technical barriers of contribution, it is the perfect platform for learning and contributing something meaningful back. We made conscious architectural decisions with an eye for contributor growth tied to technologies we felt people wanted to learn. And, revitalizing the systems happened with an eye toward a cleaner, modern architecture that would afford more straight-forward contributions without the overhead of legacy systems.

A better, more stable service offers more value. If our users get value and they continue to get value, I believe they will help sustain the project through donations or contributions. And, they can focus on the great things Drupal offers. Put differently, if people routinely experience challenges with the service or have trouble getting value from it, this lowers confidence and they are less likely to invest. SimplyTest must seek and be in a position to drive more contribution to remain viable. As such, we hope our work to build a new SimplyTest will hopefully position it to reach its fullest potential.

Another goal is to have SimplyTest be a showcase for the best that Drupal offers. It wouldn’t just be built *for* Drupal but *with* Drupal as well. If we found ways to make Drupal or it’s dependencies better through our efforts, we did so. This is how the ecosystem works and we wanted to be fully responsible for this.

Any modernization would be adding value, not losing it. We aimed to have at least 100% feature parity with the old version. I’m proud to say we achieved this goal.

Finally, we stuck to our core tenets. We remain committed to open source. The service would be and will forever be free to our users. And, our actions reflect our fundamental goal to lower the barrier of entry for those who want to use Drupal and learn about the wonderful community we’ve established. 

## Donations and Paid Labor

I don’t expect people to work for free. Some choose to volunteer and I’m really grateful for that.  But, when I took over, I had no money to pay for anything. I established an Open Collective to help with this. I began accepting donations. Initially, this helped pay for expenses like SSL certificates and various attempts to make development infrastructure. But, I saved up money to help pay for sponsored contributions. I was proud to offer some people work when they were out of jobs. I hope to do a lot more of this in the future.

Most importantly, this allowed me to spend some funds toward the revitalization. The project started to get some much needed help and velocity toward our goal. I was able to pay people with specific skills to come in and do work faster and of higher quality. 

A lot of this progress was made possible by donations of small and large from both individuals and organizations. It was really cool to also see Drupal Camps, who often leverage SimplyTest for contribution days, make donations with some of their funding. And, companies like Centarro, sponsored development of specific features (the one click demos). 

## Sponsored Backend

Our existing worker backend was a significant source of pain and suffering. It was a hand-coded, hard to maintain, antiquated, impossible to scale platform. Even though a new application was planned, we started with a backend replacement so we could exclusively focus our time on the front-end later.

Many requested the use of ephemeral architectural patterns. Issues were opened for analysis on a container-based infrastructure. However great the technology was to fit our needs, it was not feasible. The cost to move off of a monolith and into a cloud-based platform was high. The development and maintenance of infrastructure was not something I could do without significant learning. And, even if it was perfect for our needs, a cloud-based, containerized solution was both cost prohibitive and impractical. As such, we opened up a call for a sponsored solution. Elijah Lynn, Cameron Eagons, Greg Boggs, and I formed a committee to review proposals. We chose TugboatQA. We basically were given an out of the box, ephemeral, container-based infrastructure that was all driven through APIs and had nice abstractions for Infrastructure-as-Code and hooks to execute the specific Simplytest dynamic behaviors.

This was basically broken down into two phases: 

*Phase 1* - we used a repository-based approach for our Drupal 7 integration. We generated YAML files that had all of the infrastructure definition and commands, pushed the definition to a repo branch, and made use of the Tugboat CLI to invoke provisioning. Teardown was already included in our IaC definitions, so it automatically cleaned up!

*Phase 2* - TugboatQA made some microservice enhancements between our Drupal 7 integration and our new Drupal 9 launch. More APIs were created for provisioning and log management, allowing us to move away from the repository-driven approach and to drastically simplify this integration. It was also a really natural fit for the ReactJS front-end we created. 

This was my first time leading the project that I considered a vendor. I had a lot of hesitance tied to this decision, especially for selecting a proprietary tool. I will say, the introduction of TugboatQA was game changing for the health, maintenance, and viability of the project. Plus, the TugboatQA (and Lullabot) teams sponsored this work because they are also committed to open source. I feel this was a great decision with a lot of alignment for all parties involved. They have been fantastic partners.

## PaaS Hosting

With a volunteer team and limited time/budget, you need to be very careful about what you maintain with a project like this. We learned the hard way how difficult it is to maintain your own infrastructure. In my mind, you can’t waste time reinventing the wheel. While it may seem to conflict with our open source roots, we chose a service and vendor that was closely aligned with our identity: Amazee Lagoon. We are grateful they sponsored the use of their service to help run our Simplytest Drupal 9 website. While their PaaS service is a paid offering, their product is open source. And, it had relevant features and a high degree of customizability we needed to be effective. Amazee also offered use of it’s CDN services, which help with both performance and security. Worrying less about a website affords time for us to build more value into the system. We’re fortunate to have access to this service to allow us to improve the service itself. 

## Drupal 9 Website

What a better way to showcase Drupal by using Drupal itself. We wanted to harness the best Drupal had to offer as part of our revitalization. We actually started our efforts with Drupal 8 when we began to create the new application, but we then upgraded to Drupal 9. We have leveraged many cutting edge features, like the Typed Data system and the web service capabilities, which help modern Drupal applications shine. We’ve been able to leverage core features and the underlying framework to create a set of services, data models, and API endpoints that pair perfectly with our React-based front-end.

SimplyTest has also innovated significantly around the Drupal community project metadata. Because our efforts were “experience first”, we ran into challenges implementing the ideal experience in support of semantic versioning, compatibility of major versions of core within projects, and more. Major props to Matt Glaman and Benji Fisher for helping research and innovate around these challenges.

## Fresh Design

Comic Sans is a sign of the nineties, and the nineties want it’s website back. We’re happy to oblige. With a totally revamped system, we needed a modern design that best represented the technical innovations under the hood. Ana Laura Coto helped with this by producing designs for us, including a new logo! This will help our experience, allow our work to shine, and best represent how cool and modern the new system actually is.

## Updated Theme

Iris Ibekwe set up our initial efforts when we implemented the Drupal 8 theme. It was responsive, leveraged modern grid systems, and established build tooling with Gulp, NPM, and more. This work helped get the ball rolling toward implementing our new designs.

A lot of time passed from when the original theme was set up and when we got the new backend fully built. Some newer tools came out that allowed us to upgrade some of the older tools and innovate further. Matt Glaman implemented Laravel Mix, which allowed for live refresh and replaced the theming framework with Tailwind CSS.  

QED42 stepped up majorly to finish the job. Their team did a significant amount of theming work and QA. They applied some updated design revisions made by Ana Laura to address identified accessibility issues. As the backend was evolving, the theme was being completed in parallel by their team. The QED42 team got the job done and their team was a pleasure to partner with. Front-end work is one of my technical limits. I was grateful I had such great help with this area.

## ReactJS Front-end

The interface for SimplyTest has a lot of conditional behavior. It’s highly interactive. This presents our users with an experience that simplifies much of the underlying Drupal complexities. Users enter a project, they pick a branch, they then only see relevant options to them based on what they want to test. Drupal has evolved a lot and putting the experience first for our users has meant a lot of work behind the scenes to abstract complexities. This work is never done, but our new ReactJS front-end is a major step forward.

Matt Glaman created the React front-end and the connecting backend APIs from Drupal. ReactJS is a great compliment for the web services sponsored by Drupal. The React app maintains state, which can help to address conditional needs and guide users through the experience we want to offer. This was a complex task and Matt’s leadership helped make something from nothing. I am just learning ReactJS and was struggling to make the kind of progress on this we needed. Matt’s expertise was critical to connect both systems and make this a huge success. I’m far more confident that others can contribute to this part of the system and use the React app as a reference for learning (I certainly will be).

## Automated Testing

We were making sweeping changes throughout the last several months. When you add in development activities in parallel, it is much easier to break things. Thankfully, automated testing was implemented throughout our process. 

As Matt was implementing the Drupal backend and the ReactJS front-end, automated testing continued to be developed at the same time. PHPUnit tests were helping with the Drupal endpoints. Cypress was used to test all of the front-end and interactivity. Having automated tests allow us to have a stable development workflow that ensures we’re less likely to break things when pushing changes.

## Website Repository and Quickstart

SimplyTest is a Drupal profile maintained on drupal.org. But, our application runs like a conventional Drupal website managed by Composer. Having a repository with SimplyTest installed allows for more key outcomes. First, the repository maintains the Drupal website running SimplyTest.me in a conventional manner to other Drupal applications. This repository serves as the integration with our new PaaS hosting and it looks and feels just like a standard Drupal application (because, it is). Second, the repository is a quickstart for contributors to load the website locally with minimal work. Community members can readily contribute just like any other Drupal project. This helps save time for those who want to participate and don’t want to waste their time with all of the manual setup. We also maintain both DDEV and Lando support within this Quickstart, with some basic documentation we aim to continue to improve with time.

## Violinist

Again, we don’t want to waste time with manual work if we don’t have to. Matt installed Violinist on our SimplyTest website repository, which scans Composer.json files on the main branch for Composer updates. If updates are found, Violinist creates a pull request for the update. This works for Drupal core, all of the contributed modules, and even the SimplyTest code on Drupal.org. Pull requests trigger our automated tests to get immediate feedback. And, it sounds wild, but I can basically update the site from my phone. This is immensely cool and something that comes in handy for rapidly applying security updates. 

## Modern CI/CD

Our new CI/CD workflow offers smaller, incremental changes we can test iteratively before deploying to production. Our workflow with Violinist, pull requests, Github Actions, and on-demand environments on Lagoon allow us to get testing feedback, deploy small changes frequently, test them before pushing to production, and deliver with high quality. We have moved from having a monolithic infrastructure that wasn’t change friendly to being able to rapidly test and deploy changes in an ephemeral, highly automated, and change-friendly infrastructure. It’s been awesome and it’s such a sharp contrast from where we were before.

## Monitoring and Alerts

I leveraged the free version of Pingdom to put basic alerts on the website and worker backend when I took it over. I got alerted for outages, which were frequent before. All monitoring and alerting has been switched to the new PaaS website and leverage TugboatQA service notifications (and Linode as their vendor) that could impact our backend. I believe there are more opportunities to improve this in the future, but the basics are there.

## Live Coding Streams

Not only did Matt Glaman help with development and architectural guidance, he had an idea to do live streaming sponsored by his company, Bluehorn Digital. I learned a lot from these streams and am confident many others have as well. Streams cover development, testing, issue queues, development tools, and more. It’s great having someone talk through the process the entire time to understand the details. The streams were great for smashing bugs, working on new features, diving into the architecture, and advocating and promoting SimplyTest itself. They continue to be something I look forward to and were an immense help to launching the new site.

## Partners Program

Between Bluehorn Digital, QED42, TugboatQA, Centarro, and Lagoon, it is very clear SimplyTest would be in rough shape without these partners. SimplyTest would not even exist without Druid and Maloon who sponsored the legacy systems. It is equally important to say thanks and highlight their contributions to the project, so I established a partners program. For companies who continue to invest in SimplyTest, we will continue to recognize you and offer incentives as we are able. One incentive is the “first right of refusal” for sponsored SimplyTest work. Partners get first dibs when we choose to pay for enhancements or bug fixes. Please see my previous blog post on the topic to learn more about the kinds of partnerships we’re offering.

## Social Media Presence and Talks

It is incredibly important to engage with the community. We sincerely want to know what you think, where we can do better, and how we can deliver the best service possible. Thanks to AmyJune Hineline, we have established a Twitter presence, we are active on our Drupal Slack channel, and we have given talks at several camps that have highlighted our plans and why we’re doing this. AmyJune routinely uses SimplyTest as part of new contributor workshops. Because of this, we see much more engagement. Users routinely file issues, send messages, offer ideas, and help us be better each day. We’ve seen donations from the community. It’s such a stark difference from when we had no presence when I took over the project. And, AmyJune has been a critical part of helping establish and build this community from basically nothing.

## Contributors

There are too many people to thank that helped us get where we are today. And, this was a collection of things that led up to the big reveal of our brand new Simplytest.me application. None of it would have been remotely possible without several people and companies stepping up to help. I mentioned several people already in this post and there are countless more who cheered us on, offered advice, pitched in, made donations, and so much more. This effort is no longer “my” side project, it’s now “our” community project. Thank you, thank you, thank you.

# Parting Thoughts

We have finally put SimplyTest back in a good place. This is worth celebrating. Our technology is best-in-class and is appealing for anyone to use or learn. We managed to drastically reduce the code and simplify the application, lowering the barrier of entry for SimplyTest itself. We reduced maintenance activities down to nearly zero for both the application and the underlying infrastructure to allow focus on value creation. We’ve built a community that has promises of growth. And, we have the tools in place to sustain it. In retrospect, all of these small steps have added up to something significant in the few years I’ve led the project. It truly was a team effort. I couldn’t be more excited to finally be at this point and share this with everyone. I am grateful for those who pitched in and even more happy to say, “we did it.”

This whole thing has taught me a lot. In a lot of respects, SimplyTest is both the best and the worst of open source. It’s not only a free service but all of the code is open sourced. It’s a great example of both companies and individuals pitching in toward a common cause. But, after having led these efforts, I have seen first hand how people can treat open source maintainers when they get behind a keyboard. Some users expect a lot but fewer are willing to pitch in and make it a success. Our system remains largely volunteer-led, donation funded, and services sponsored. We’ve been highly resourceful with what we have (which is very little in the grand scheme of things). At times people just seem ungrateful. On a personal level, I wish this was more harmonious. I’d love for more help (financially or through direct contribution). I’d love for more awareness for those who expect more than we can reasonably offer. Regardless, we try to put our users' needs at the forefront of the service. We welcome the challenge to serve everyone. And, we are in a much stronger position to serve people *now* but it took so much time and effort to get there.

Another lesson in open source is how hard it is to have a big impact without resources. Working alone requires investing a lot of time and effort outside of your day job. It’s a fast way to burn out. SimplyTest.me historically relied on volunteer labor, sponsored systems, and had no money. Druid and Maloon graciously paid for all of the web, worker, and proxy servers. But, without funds, we couldn’t pay to get help from subject matter experts when it was needed. We just had to roll up our sleeves, work hard, figure things out, and be really scrappy. We picked up the phone to call friends when it was urgently needed to keep things running. But, one can only do this so long. And, I became fully aware of why the previous maintainer decided to move on. A large portion of time was focused on incidents and “keeping the lights on” while wanting to build the future. Wholesale change was needed and it makes it even more rewarding to launch our brand new system.  

One more side note… the largely volunteer Drupal community is an amazing example of what can be accomplished at scale. A small number of contributions by a lot of people can add up to something significant. And, yes, SimplyTest is a part of the community. But, SimplyTest certainly has not seen the vast contribution that the Drupal ecosystem benefits from. We will continue to aspire to reach and achieve the kind of scale the broader community benefits from.

# The Future

We need to grow into this new project we just launched. We just shed a ton of technical debt and can finally breathe easier after a rough few years. We still have a lot to learn and improve upon, and we need to work out the bugs. It was a lot of change in a (relatively) small amount of time, but we feel confident in the decisions made and to put us in a position of success. It’s incredible what a small number of highly motivated and capable people can do with clear goals, clear strategies, and clear purpose.

In the coming weeks, I will be publishing a quarterly roadmap talking about key objectives we wish to hit moving forward. We will start with a pause in new features to fix bugs, stabilize, and identify improvements. We will then announce a prioritized set of features which will be informed by the feedback we get.

We thank all of you who supported the service through our transition and when the system did not live up to your expectations. We’re confident that the future is bright, and we look forward to having SimplyTest serve the needs of the community for a very long time to come.