---
title: "SimplyTest.me and Google Summer of Code 2019"
date: 2019-03-07
slug: "simplytestme-and-google-summer-code-2019"
tags: ["drupal", "people"]
description: "SimplyTest.me is participating in Google Summer of Code 2019 — here's what students can work on and why it matters for the project."
draft: false
---

[SimplyTest.me](https://simplytest.me/) is a project I continue to lead and volunteer my time to. I’m driven to help lower the barrier to entry for people in our community to contribute, use Drupal, and be a part of our community.

For me to be effective, I need to keep my eyes open for unique ways to help the project. Much like our larger community, we must be opportunistic to remain sustainable. [Google Summer of Code](https://summerofcode.withgoogle.com/) (GSoC) is just that. I previously participated as a mentor, helping students port security-related modules to Drupal 8. I was approached by Matthew Lechleider ([slurpee](https://www.drupal.org/u/slurpee)) to see if there would be a fit for SimplyTest.me. And while SimplyTest.me is unique in that it is both an open source project, a set of services, and associated infrastructure, it has long been a desire of mine to have more people contributing and have SimplyTest open up career opportunities for participants. GSoC is just that.

According to the [GSoC timeline](https://summerofcode.withgoogle.com/how-it-works/#timeline), student candidates are participating in the application period. For Drupal, specifically, they are not only [evaluating project ideas](https://groups.drupal.org/node/534703)but [getting comfortable with community standards and contribution](https://www.drupal.org/node/2415225). Candidates then write up proposals for the GSoC leads and project maintainers to evaluate. Matthew summarized this perfectly by saying,

> *GSoC can be similar to a "choose your own adventure" type summer job*. *We provide cool bosses (mentors), a software platform with a request (Drupal/SimplyTest.me), and the option for student to build their own project plan then execute project while being paid via Google.*

But, given the fairly niche nature of SimplyTest, a simple project description is hard to develop a proposal. This blog post helps expand on the project description to help clarify potential next steps.

##  

## What does SimplyTest offer?

Any student participating in this GSoC project would get a much broader experience than other projects potentially offer. And, while we have a current Drupal 7 based system with a highly customized infrastructure, this project will emphasize our future roadmap in a fresh, new system. This features the following modernized architecture:

- A Drupal 8 distribution

- Integration with Drupal.org sponsored web service APIs

- A React.JS front end application

- DevOps efforts (Docker, web service APIs, infrastructure as code)

- Integration with Tugboat QA (this is still formally TBD, but a proof of concept in the old system is near completion)

## Project ideas

I want to stress that we need to make progress on the new system, not the current one in place. The following serve as some high-level ideas and “current state” of known needs. I will stress that a successful project proposal should reflect the necessary research and details needed to achieve the following ideas. The links below offer further details and insights helpful for an informed project plan.

- [Implement Tugboat QA](https://www.drupal.org/project/simplytest/issues/3036569) - The proof of concept is in the current Drupal 7 system. A Drupal 8-based equivalent will need to be developed. This may include porting the Tugboat QA module to Drupal 8. Students should research this platform and the current proof of concept to get an idea of the work needed.

- [React.JS front-end](https://github.com/nerdstein/simplytest/tree/8.x-4.x/themes/simplytest/react) - The distribution will have a series of API endpoints which cache data from Drupal.org. These services may need built or enhanced to work with the new React.JS front-end, which is in progress but will likely need to be finished. Students should look at the work-in-progress Drupal 8 code base for an idea on current state.

- [Implementing the Drupal 8 theme](https://github.com/nerdstein/simplytest/tree/8.x-4.x/themes/simplytest) - Our distribution already has a Drupal 8 theme in place. However, it needs to be implemented with the React.JS front-end and applied more generally throughout the Drupal system (e.g. menus, header, footer, FAQ page). Students should look at the work-in-progress Drupal 8 code base for remaining efforts.

- [Feature parity](https://github.com/nerdstein/simplytest) - There are many [Drupal 7 specific features](https://cgit.drupalcode.org/simplytest/tree/) that would need to be ported for feature parity. Some current features are no longer required given the Tugboat QA integration. Students should evaluate the Drupal 7 distribution and articulate missing, but relevant features that can be accomplished in the project.

- Analytics - New mechanisms will need to be in place to develop various usage-based reports from within Drupal 8. Students can share potential approaches to achieve this goal.

Please note that once we get a stable set of features, the Github repository will be moved to a 8.x branch on Drupal.org.

##  

## Conclusion

I look forward to seeing student proposals and am more than confident SimplyTest.me provides both a level of rigor and educational opportunities. I am also interested in potentially splitting this up into two projects: front-end and backend/DevOps. Any interested students can reach out to me via [my contact page](https://www.drupal.org/user/1557710/contact). Other potential mentors have been identified that have worked on SimplyTest.me and discussions are ongoing.