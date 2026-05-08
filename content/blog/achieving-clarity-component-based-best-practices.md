---
title: "Achieving Clarity in Component-based Best Practices"
date: 2018-04-02
slug: "achieving-clarity-component-based-best-practices"
tags: ["development", "drupal", "people"]
description: "Here we are. It’s been over a year now that our community has explored design components (integration of design systems, pattern libraries, etc) and Drupal."
draft: false
---

## Introduction

Here we are. It’s been over a year now that our community has explored design components (integration of design systems, pattern libraries, etc) and Drupal. The community has shared different tools and solutions, presentations from many individuals representing different companies and perspectives, and processes/workflows that enable the different teams and disciplines. I would classify the time spent to date as research, exploration, and innovation. While this is expected for something new, we need to define best practices. The purpose of this blog post is to help us start a conversation to have guidelines and principles we can use to have better discretion when developing component-based solutions.

## Context

I got curious and started exploring Drupal’s Component-based landscape after reading several blog post around the time of NERD Summit 2017. I got more serious at MidCamp 2017, where I saw a great presentation on components by [Brian Perry](https://www.twitter.com/bricomedy). What was surprising to me about Brian’s talk was the amount of contributed solutions he presented. He shared solutions that made use of Paragraphs, UI Patterns, and more. At the same time in the community, members were creating tightly-coupled contributed themes that packaged a pattern library (design system) within a Drupal theme. Many had the same foundational implementation but minor variations for different task managers (Gulp, Grunt, etc) and different CSS frameworks (SASS, LESS, etc). As I [previously wrote about](https://nerdstein.net/blog/exploring-simplicity-drupal-design-components), I desired to explore a simple approach that differed from that which other community members were taking and achieved the following goals:

 

1. A stronger use of Drupal Core and addition of contributed solutions only on as-needed (at this time, tools like “Place Block” and the Layout Initiative were just coming onto the scene)

 

2. A simple, clearly defined process/workflow for a creative team and a technical team to collaborate across two different disciplines

 

3. A fully decoupled, separation of the systems with a pattern library capable of promoting DRY principles across more than one site (and potentially even technical platform) within an enterprise

 

My intent was providing a fresh, unbiased look at achieving the goals. The community was largely silent.

## The Now

In my blog post, I proposed a solution that I felt achieved the goals at a high-level. I knew it did not solve every detail someone would encounter. Throughout the year, I had continued discussions with Brian Perry and followed his efforts. We routinely highlight the different needs of different users, like designers, site builders, developers, or themers. All have varying skills and we tried to understand the selective approaches that could be used cohesively. Fast forward to MidCamp 2018, which happened this past weekend (as usual, the MidCamp experience did not disappoint). Up to this point, I had very little engagement from my blog post. However, I learned that the AMA and Palantir teams not only read my blog post, but deemed my approach “The Nerdstein Method.” They explored the use of it in-depth (I was shocked). A session ended up being cancelled, which led the MidCamp organizers to request a components-based panel with Brian and I. I was already looking forward to catching up with Brian again in person. The panel ended up being one of the most fun things I have done in recent memory.

 

The main point of the panel and common theme in all of the related discussions is that there still is a high degree of learning and fuzzy best practices in this space. Brian mentioned a proposed DrupalCon panel that had a name like, “[Component-Driven Development: The Awkward Years](https://events.drupal.org/nashville2018/sessions/component-driven-development-awkward-years),” which, to me, basically summarizes the immaturity, learning, and growth our community has experienced for component-based solutions. We need to move past this -- both with technological advancements and knowledge of the space. Aside from just defining potential approaches, there is still a high degree of discretion when building solutions that can make or break an implementation. I want to share findings from the discussions had at the camp, which I hope can help solidify ways to think through decisions.

## Practices

The following items represent ideals I believe our community should strive to use. Situations change and there are always practical reasons to not do these things. However, this should be done with awareness and decisions should be made consciously.

### Data Normalization Principles

Based on Atomic Design, it may seem like an obvious best practice, but patterns should be broken down into their smallest possible form.

 

When I was in school and was a faculty member at Penn State, I routinely discussed a related concept of data normalization as a foundational aspect of structuring data. While this is [most routinely discussed with databases](https://www.guru99.com/database-normalization.html), patterns in a design library represent similar considerations. First normal form requires that each “field” maintain a single value. Think of an address. You could store an address as one field or you could store separate fields for a number, street, city, state, postal code, and country. To observe first normal form, separate fields would be used in a database.

 

With a pattern library, there is conceptual overlap for atomic design principles. Patterns should be broken down into the smallest parts and these are commonly atoms in the pattern library. This is akin to first normal form. Atomic Design reuses the most discrete atom patterns to set up subsequent molecule, organism, and page patterns (DRY principle). Second normal form discusses the use of “foreign keys”, which complements the concept of reusability. Conceptually, you break down higher-order patterns to their lowest forms, which will likely boil down to a series of atoms. If patterns are not broken down into the smallest possible elements, this would both violate normalization principles and likely limit reuse.

### Least Responsibility Principles

I’m not a huge advocate for strictly abiding by theory, but it is critical to understand the purpose of the two systems. Provided you have a design system like Pattern Lab and a content management system like Drupal, what responsibilities should these two systems have?

 

Pattern Lab should be as high-level and implementation agnostic as possible. To achieve this goal, it needs straight-forward and simplistic representations of data and very little, if any, parsing. The end result should be very basic Twig templates, limited use of “macros” or Twig functions, and a higher-order definition of the data expected. Macros or functions should only represent standard processing, but using macros or functions to perform CMS-specific transformations is incorrect. Pattern Lab can define the expected data to guide any CMS, which should reduce the need for transformational processing.

 

Drupal, on the other hand, manages the data and owns whatever transformation is needed for its data to align with Pattern Lab’s expected data representations. Within its Twig files or preprocessing, Drupal can perform the data processing. Drupal owns this burden for two primary reasons:

 

1. If you ever want Pattern Lab to support more than just Drupal, it does not make sense to perform any Drupal-specific processing in Pattern Lab.

 

2. Implementation-specific processing in Pattern Lab can damage reusability (and introduce complexity), as the processing may only address specific use cases. Additional similar patterns will start to creep up with their own processing of, basically, the same end result.

 

The complexity of Pattern Lab templates should stop at the native Twig templating system, which includes loops, conditions, and includes. Any implementation-specific functions (custom Twig functions) would need to then be mapped back to your CMS systems and would likely introduce even more complexity in the mapping between the CMS-specific templates and the expected design library implementation.

 

To summarize:

 

1. The pattern library should have very simple data, very simple templates, and be the source of truth for visual specification (CSS, JS, image assets, etc)

 

2. The content management system should maintain its own ideal data structures, manage the parsing of its data structures into the pattern templates, and subsequently pass the parsed data as a mapping to the patterns found in the pattern library.

### DRY Principles

Implementations in Pattern Lab and Drupal need to be viewed as completely separate. Drupal can and should reuse Pattern Lab artifacts as much as possible, which is exactly why the Pattern Lab implementation needs to remain as simple as possible. The same Pattern Lab pattern could be used in Drupal by Views, Custom Block Types, or anything that can be rendered by Twig. Complexity within a Pattern Lab pattern could limit broader application. Because the systems are separate, there is discretion on how the Drupal system implements the patterns found in Pattern Lab.

 

One major misunderstanding is that there should be a one-to-one mapping of patterns between the two systems. This is completely false and violates the DRY principle. As an example, what happens if Drupal has a listing rendered by a View and a listing rendered by a custom block type that both have the same design guidance? Do we need to make another Pattern Lab pattern for both cases? This violates DRY principles. I want to explore considerations around the DRY principles a little deeper.

 

First, Pattern Lab should demonstrate various uses/examples of the same pattern through the [variants](http://patternlab.io/docs/pattern-pseudo-patterns.html) feature. Each team needs to thoughtfully collaborate to understand when it’s appropriate to make a new pattern or to use a variant of an existing pattern (e.g. [a proposed exercise](http://alistapart.com/article/from-pages-to-patterns-an-exercise-for-everyone) by Charlotte Jackson). To extend this even further, the data in variants can represent both content and configuration. Content can show a listing with items that have images or items that do not. Configuration can represent different states that need to be observed for conditional logic (e.g. a boolean variable for showing an image conditionally) or different CSS classes that need to be passed for known use cases (e.g. having the same pattern with a blue, green, or red background). Leveraging variants helps with DRY principles because:

 

- It lessens the complexity of the pattern library by reducing the number of patterns

- Each pattern has self-contained examples of how patterns are expected to be used

- The same pattern can maintain variants for multiple uses

 

Second, there is a high degree of discretion and a ton of flexibility in how Drupal can use patterns defined in the pattern library. Because there does not need to be a one-to-one mapping, engineers must build the best architecture in Drupal that matches the specifications regardless of what patterns exist in the pattern library. The two systems are completely decoupled and Drupal already offers a substantial number of ways to implement the requirements (content types, Views, View Modes, custom block types, etc). As Brian noted, integrating the patterns into the UI Patterns module actually serves as documentation for how components are intended to be used within Drupal.

 

Engineers not only have a high degree of flexibility in the Drupal architecture, they have a high degree of discretion in the use of mapped patterns from the pattern library within a Drupal template. As such, this does not explicitly need to map to one atom, one molecule or one organism. A combination of one or more lower-order patterns may be mapped in the same Drupal template. This is used for items like Views, which may have a title, listing, and a potential pager. All of which may be three separate patterns in Pattern Lab. The highest order patterns, like those that represent full pages, are often not brought into Drupal at all because a component-driven Drupal “page” is often comprised of one or more block instances, Views, attributes of a content type, global elements, and much more. Should the patterns be sufficiently flexible (previous point), Drupal best practices can be leveraged without concern from the library and promote the use of reusable patterns that leverage both content and configuration variations in a highly-extensible manner.

### “Right tool for the right job” principles

The “Nerdstein Method” has emphasized an approach that is still pretty technical. Implementers basically need to be comfortable programming (e.g. template mappings, Drupal-specific data parsing, and using Composer). With some limitations, similar goals can be achieved with site building and a stronger use of contributed solutions. This is where the use of Paragraphs, UI Patterns, or Display Suite can be incredibly helpful for teams that want to avoid custom code. Please note that the ideals I am sharing may not be fully possible through the use of contributed solutions and it’s difficult for me to predict how far the mileage is because I am comfortable with an approach based on custom code (in fact, I find it more straight forward).

 

Leveraging the right tool for the right job should include an acknowledgement of standards. Observing defined standards like BEM,SMACSS, and others can help ensure the work done in both the pattern library and CMS are as portable as possible. This eliminates headaches and can encourage broader participation, as the work is performed in a conventional way.

## Summary

Here we find ourselves in a community where we have explored the space of Drupal and component-based design systems. It is my hope that by surfacing some potential best practices I’ve observed, this can both help provide some guidelines for others and facilitate a discussion to help move this definition forward. I hope others share things they have learned to move past these “awkward years” as soon as possible. While it’s been great for innovation, we need to commit to sharing knowledge and surfacing best practices to move forward.

 

I also want to thank my awesome team at Hook 42 for sending me to MidCamp and allowing me to be a part of the great event. Special thanks to Brian Perry and Chelsie Johnston for their contributions to this post.