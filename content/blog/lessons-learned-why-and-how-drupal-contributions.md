---
title: "Lessons Learned: The \"Why\" and \"How\" of Drupal Contributions"
date: 2016-10-21
slug: "lessons-learned-why-and-how-drupal-contributions"
tags: ["development", "drupal", "people"]
description: "I am ashamed to admit, for the longest time I used Drupal (heck, even complained about it) but contributed absolutely nothing back."
draft: false
---

## Why

I am ashamed to admit, for the longest time I used Drupal (heck, even complained about it) but contributed absolutely nothing back. It occurred to me that, not only did I learn technical and marketable skills thanks to Drupal, my Drupal experience directly corresponded to opportunities that supported my livelihood and viability for me and my family. And, all of this occurred without one line of code from me contributed back.

 

A long while back, I decided to make an effort to solve a core issue. At that point, I had stronger SVN experience than Git. I had approximately eight years of experience in PHP development - most of which was in building custom solutions completely outside of development frameworks. To my surprise (and naivety), I was met by critical feedback on the work I did. And, looking back, this was rightfully so. I was clueless about how complex Drupal core was and the thoughtful community practices I didn't understand. I likely embarrassed myself, but was slightly offended and crawled back into my comfortable Drupal development cave.

 

After many more years of using the tool and after I constantly dismissed the work I did as "capable of being contributed" -- I reconsidered. "This was too custom" or "I didn't develop this in a way that others could use" were popular excuses I made. Finally, about two years before Drupal 8 was eventually released and was becoming something I wanted to learn, I decided to try contribution again. I was hungry for the opportunity to learn the tool and knew Drupal 8 experience was rare (at the time) but highly marketable. I also knew having no contributions on drupal.org was not marketable and didn't reflect my competency with the tool. I knew nothing about Symfony at the time. I had object-oriented experience from Java development. But, the discussions and reading I had done to date proved substantial gaps in my understanding and were intimidating. But, I didn't want to make the same mistake I made before. As such, I felt contributed modules were more appropriate than an attempt to dive back into core. At that time, many useful modules needed Drupal 8 ports. I knew many folks that didn't have time to port theirs and my Drupal development experience made me more familiar with the problem solving needed to leverage core's APIs (not develop them directly).

 

This shift toward contribution-friendly development has made me a better developer. I now give back by default and I have changed the way I solve problems from one that is specific to my implementation to one that solves smaller, more discrete problems in a reusable and contribution-friendly way. I get a ton of energy from giving back and it's fascinating to me to think of the many ways my code will be used in the world. I now maintain many different modules on drupal.org (really only the Drupal 8 versions) and I try to give back to any project I use as I run across a limitation or bug. I now feel like a part of the community. And, if you get one thing out of this post, **you should do it too**.

 

## How

I now regularly connect with others in the Drupal community (and love it). I present at conferences, I participate in issue queues, I'm on IRC, and I remain active on social media. Through these connections, some community members new to contributing have posed the question: *How do I participate?* First, let me admit that I am constantly learning better ways of doing things and this is not a definitive list. Let me also acknowledge there are countless people that have been doing this longer than I have. I hardly consider myself an expert, but the posed question made me reflect on my past experience.

 

**Get a drupal.org account**

To start your journey, create a drupal.org account. Fill out your profile information and add a picture so there is a face to the name. 

 

**Find a mentor**

It's almost a guarantee you will have questions or you may get stuck on something technically complex. You may need to bounce ideas off of someone or may have a question on what constitutes best practices. You should have someone willing to chat on IRC, email, Slack, or get on a call for an open discussion. I'm so fortunate to have folks like Kris Vanderwater, Tim Plunkett, and countless others from both Acquia and CivicActions that have served in that capacity for me. Credit your mentors by adding them to your drupal.org profile.

 

**Find a module or theme project **

There may be points of frustration while you are learning. Pick one project that you use regularly, have interest in, and one that is not wildly complex (until you get your confidence). Become an expert with the specifics of the project. Work toward building the trust with the project maintainers. Your contributions may lead to becoming a project maintainer. You will get bonus points for selecting a mentor of a project you want to participate in, as this person knows the project and can more effectively help get you ramped up.

 

**Set up your local system**

You will need a sandbox set up to do the work, you'll likely want a modern IDE (this can be a huge help for debugging, coding standards, and more), and you'll want to set up Git. You will need to clone the project repository, set up branches per issue, and learn the best practices of using Git to do this work.

 

**Work on issues and patches**

This may seem obvious, but pick up an open issue in the project and submit patches. Start small by picking up a novice issue. Assign yourself so others know you are working on it and follow up with a comment. You will get familiar with Drupal.org's version control system, generating patches from Git, interdiffs, the process and conventions of working within issues (needs work, needs review, RTBC, etc), and you will see how others review your work in the community. You could even ask your mentor to chime in if needed. In the event you have questions on how to do this, these processes are well documented on drupal.org and it's good to learn how to dive into the documentation.

 

**Coding standards**

Before submitting any patches, make sure you set up your development environment for coding standards. This, too, is well documented on drupal.org and you can see my blog post on how I set up my local environment to integrate Coder libraries, PHPCS, and PHPStorm.

 

**Crediting**

After you submit a patch, ensure you and your organization get the recognition you deserve with credit. This will bolster both your drupal.org profile and your organization's page. By accident, some maintainers forget to click the checkbox needed to credit the issue, so keep an eye out for this and remind the maintainer if your patch gets used (even in part).

 

**Keep going**

Once you finish with your first issue, pick up more. Slowly branch out into issues found in other projects both by use or your interest. Create your own issues for bugs you find or improvements you think are worth making to projects. Your skills will grow by solving diverse problems in a contribution-friendly way. 

 

## Conclusion

There are many reasons for writing this post. I hope the tips and tricks I have learned are useful. I also aim to help provide motivation for those that may think they can't do this or to speak to those that lack the confidence to dive in. Further, I hope I can inform people to avoid the mistakes I have made. May it serve in a small way to help bring both more contributors and ones that can skip past the pain points I've already experienced. We all need some sort of a launch pad and a frame of reference to help us get started. Participation can be intimidating, but it certainly is driven by a sense of purpose and a desire to improve.