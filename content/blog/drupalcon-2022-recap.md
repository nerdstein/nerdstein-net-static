---
title: "DrupalCon 2022 Recap"
date: 2022-05-09
slug: "drupalcon-2022-recap"
tags: ["development", "drupal"]
description: "A DrupalCon 2022 recap covering Drupal's competitive position, the state of SimplyTest, and what I'm looking forward to next."
draft: false
---

It has been a while since I wrote a blog post and it's an acknowledgement that I dialed back some of my normal Drupal community involvement. Between several years of maintaining and rebuilding SimplyTest.me on top of my personal and professional obligations, it was good to take a break. I have since been promoted at Acquia and invested a lot there. I’ve also enjoyed time with my family, and recently got a puppy. I feel it is now time to look ahead.

## State of the Project

I was in the first in-person Drupal Camp in Florida a few months ago. I presented a talk evaluating the landscape of Drupal competition. I tried to present data-centered, objective research with a perspective that cut through opinionated nonsense I saw on the web. I categorized competition into frameworks, open source/proprietary, and PaaS/SaaS positioned. Having done so, I learned a lot about Drupal’s identity in the world and where it could better compete outside of it. Unfortunately the talk ended up not being recorded but [I have linked to the slides](https://nerdstein.net/sites/default/files/presentations/Evaluating%20the%20Landscape%20of%20Drupal%20Competition.pdf).

While the CMS and DXP framework space is exploding, Drupal’s adoption numbers are trending down overall. While the talk covers this in greater depth, there were a few primary reasons my research uncovered:

- A heavy focus on an extensible, ambitious development framework de-emphasized builders and adopters who want low/no-code solutions and are concerned with time-to-value

- Frameworks are positioned for an enterprise market, where extensibility is critical to business success.

- Adoption is favoring tools that have more SaaS-based delivery (including products that deliver Wordpress) because they address SMB needs: faster time-to-value, common everyday features, usability over extensibility, no-code, and no/low maintenance offerings.

Major questions around Drupal’s identity (mission, vision, purpose) reflected in market conditions where adopters didn’t really know what Drupal was supposed to do given the flexibility of features of Drupal and extensible framework could be leveraged to implement a high number of use cases across many different verticals and segments.

I made a claim during the talk: to grow and become more viable, Drupal’s positioning and value must be clearer and move outside of just the developer ecosystem.

## DrupalCon 2022

The buzz from the community was palpable. While attendance was roughly half of a “normal” DrupalCon, the community definitely showed up. I was impressed the numbers were as high as they were; you can tell how much people care. It was clear the community needed this event to restore connection. Being able to see so many co-workers and friends I didn’t see through the pandemic was heartwarming. And, while there were several safety precautions in place, it was so nice to share warm embraces, grab a beer, and be able to say in-person, “wow, I missed seeing you!” I give the Drupal Association a lot of credit for rising to the challenge of an in-person event in the pandemic. I thought it was an overwhelming success.

One of the undertones of the event was the important question of where the community is going. The mission of “ambitious digital experiences'' was ambiguous and seemed to be losing steam in positioning Drupal with a clear identity or to address the current market needs. A highlight of the event, for me, was the Driesnote. I felt it not only answered the questions, but it was one of the most impactful Driesnotes to date.

Dries proclaimed the mission of ambitious digital experiences complete. There is plenty of evidence to support this. Drupal’s framework has matured for the years with several major versions (8, 9, and 10) after a major modernization to support the broader PHP ecosystem and updated practices. Data has demonstrated that Drupal, with its robust framework and large number community-maintained projects, performs very well and has vast adoption in the enterprise (see my slides for details). While one can argue that maintaining ambitious experiences is likely never done and Drupal is certainly not “perfect,” Drupal itself seems to have met the criteria set out when this mission was created.

So, what is next? Dries set a new vision for ambitious site builders. This is in homage to Drupal’s site building capabilities, which historically put Drupal on the map. Drupal 7 saw a massive rise in adoption by hitting the market in strategic ways. Tools like Content Types (structured content/data modeling) and Views (dynamic content listings/output formats) offered no-code ways to assemble Drupal. Drush (run-time automation and DevOps) and Features (configuration management) also hit key market needs. Both were further extended in Drupal 8 with the configuration management initiative and adoption of Composer. With the architecture and capabilities in place, Drupal is now reclaiming its commitment toward the site builder persona.

My immediate response was a concern that this would be perceived as moving away from the developer persona. I think this is false. Drupal has and will continue to be an amazing framework that will see enterprise adoption for these reasons. The framework is the key enabler to power the new site builder mission. In addressing more low/no-code outcomes, Drupal can enable those with less programming skills and expand into new markets. Automatic Updates provides a way for site builders to update Drupal sites without knowledge of Composer. Project Browser provides discoverability and installation into community projects for common use cases. And, now there is more.

Starter Templates stood out as a major improvement. Distributions have[had rough edges](https://www.drupal.org/project/ideas/issues/3155656). They require ongoing maintenance from maintainers. Adopters are fairly locked into the features of the distro. And, distros do not have natural Composer integration today. One major benefit of using a distro is upfront, faster time to value: you get a complementary set of features enabled out of the box. A starter template offers just that but does not lock you into the distribution thereafter. This can actually be a greater benefit for harnessing Drupal’s extensibility without adhering explicitly to the distribution. I spoke to several agency leaders and distro maintainers that said they already do this and are looking forward to using this in favor of distros. I think this may ultimately lead to deprecating distributions.

I also felt that it was a strategic benefit to move projects into Contrib to have a smaller core. We should be doing this exercise routinely as the demands of the web evolve. Core has the highest standards and it should have the most critical features only. Removing modules from core hopefully affords more time since it is less to maintain. I would argue that we should also consider bringing in some of the most prominent Contrib features, like Path Auto, to benefit from the standards and interoperability afforded by Core. If people are using something, there is a clear need.

## What is next

Dries was upfront in sharing that his plans were a pragmatic, two-year plan that didn’t look too far ahead. This is smart, as the market is fast evolving. It’s always good to not overcommit. But, what else should Drupal be evaluating moving forward?

**No-code theming** - Drupal just launched amazing new themes in Claro (admin) and Olivero (front-end). While both harness modern front-end practices, deliver on accessibility goals, and give Drupal a long-awaited fresh coat of paint, it does not yet compete with Wordpress which offers many no-code configurable themes that can enable site builders to style a website without a custom theme. I think this should be heavily emphasized as an out-of-the-box Drupal that would not warrant any custom theming. Drupal could address a key differentiator from its largest competitor.

**Usability** - Drupal cannot just focus on features site builders need, it needs to focus on the usability itself. The experience of building in Drupal is still daunting with the sprawl of features it can be assembled to deliver. A common example is the Views UI; it is incredibly powerful but can be challenging to learn. Many SaaS based tools have emphasized ease of use through inline help, highly interactive user interfaces, and very clear documentation to fall back on. Drupal will need to address this to compete.

**Marketing** - Site builders need to see first hand why Drupal is great. We must tell our story. This goes back to the identity. We need videos, marketing, and promotion of all of the great features Drupal offers site builders. They should know how to model content, create Views, develop View Modes, and understand Blocks.

**Layout Builder** - I still think this is one of Drupal’s best features with the most potential. But, competitors like Elementor, Wix, and Squarespace have crafted modern, highly interactive experiences that focus on usability. I would love to see Drupal revisit this feature given how relevant this feature is for content authors.

**Paragraphs/Blocks** - Drupal should consider addressing the component-based problem once and for all. Paragraphs offers more features than Drupal’s native block system but they are incredibly similar. The gap needs to be resolved given we have two overlapping features that are heavily invested from the community. Core should consider adding features to address this gap and ensure blocks can address more predominant use cases.

## Quick Hits

- Angie Byron, webchick, won the Aaron Winborn award. It was amazing to see a long-time mentor and friend win, as she has been deserving of such recognition.

- Amazee.io offered really cool swag with custom dog tags and collars, while Acquia made donations to help community members in Ukraine.

- A Darth Vader bagpiping unicyclist blasted the imperial march into the Pantheon party, ensuring attendees got a true taste of Portland’s weirdness. (yes, this was super cool)

- I got so many t-shirts I had to ship them back.

## Recap

DrupalCon reinvigorated the community with both new direction and long awaited connection. I feel the pivot will help Drupal address new markets and be more competitive. It should be a fun couple of years as Drupal takes on the new mission.