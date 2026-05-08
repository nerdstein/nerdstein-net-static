---
title: "Static and Dynamic Capabilities of Design Systems"
date: 2018-08-15
slug: "static-and-dynamic-capabilities-design-systems"
tags: ["development", "drupal"]
description: "It’s a classic computer science concept: Static versus Dynamic."
draft: false
---

It’s a classic computer science concept: Static versus Dynamic. This fundamental concept is what separates content management systems from static HTML, as a practical example. But, how does this apply to design systems like Pattern Lab and any system(s) that consume Pattern Lab artifacts?

 

The key point to understand is around anticipated changes. What aspects of a pattern can change either based on application, anticipated updates over time, or their conditional placement? Understanding what changes are possible help drive decisions on the use of static or dynamic. Bear in mind, each pattern can and should have static and dynamic aspects -- this is not all or nothing. This is looking at each aspect of a pattern and providing a deeper understanding of its use. These are key considerations for effectively building a design system and analyzing how the design system is consumed by other systems (potentially).

 

## How is this exemplified?

 

Let’s look at some common patterns:

 

- Search bar in the header: In many cases, these patterns are placed globally and is consistent on all pages. For consistency, the styles, markup, and imagery are often the same across all pages, which would be considered static. The text entered in the search, as an example, may change and should be considered dynamic.

- Social media icons: This has a bit more discretion and likely ties to your consumers. Does each consumer have their own social media presence? If so, aspects of this patterns need to be dynamic. If the networks and accounts are the same or infrequently change, leveraging a static approach seems practical.

 

## Understanding change

 

Something statically defined does not necessarily mean that it cannot change over time. It’s the impact of making a change and an effort to be pragmatic. Building something statically in a design system is an acknowledgement that the design system owns the responsibility for something, not the system consuming it. Changes can be made to the design system over time. There is a degree of discretion for creating static definitions that considers the frequency of changes, varying needs of the consuming systems, and more. Routine changes are a good marker for dynamic requirements. Bear in mind, static changes will require code-level considerations. Observing the best practices I mentioned in my previous post, this would require a new release of the design system and remediation in the consuming system. This is a lot of overhead when a desired change may be a simple content fix.

 

## What aspects of a design system are static?

A tool like Pattern Lab offers two primary approaches for static definition.

 

- Static technical artifacts (CSS, Markup, Assets): Design systems are built on DRY principles: consistency is key. This consistency is driven through code and assets, which are inherently static to maintain a degree of uniformity. When you create a pattern, you build the CSS, the markup, and even relevant assets like images. These natively do not change and therefore I believe they more closely align with static functionality.

- Static pages: Full page patterns often show an end-to-end representation on how patterns are applied to entire pages. This is entirely static and, in my opinion, is often just used for a representation and not consumed by other systems. This philosophy may be changing based on static site generators capable of manipulating data differently than CMS systems. This is due to the fact that a page is often comprised of several data elements (menus, titles, header elements, footer elements), which are commonly split out into separate elements of content management systems. As such, page-level patterns commonly have static elements and commonly are comprised of other lesser order patterns (which have their own degree of dynamic capabilities).

 

## What about dynamic features?

 

To reiterate, the key framing is exploring what parts of a pattern can change.

 

- Data: JSON files, found in patterns, are supposed to mock up dynamic data. Variations of multiple data representations can exist per pattern in the design system, highlighting various dynamic use cases. The consuming system is able to supply its own data, which is rendered within the statically defined markup and styled by the statically defined CSS. While the data model may be defined statically, the data itself represents dynamic capabilities.

- Conditional markup: Templating engines like Twig have the ability to render different markup based on the data passed to the pattern. This is great for handling more variations and pattern reuse (which is more pragmatic in lowering the technical debt).

 

## Discretion is key

 

There is no single right or wrong answer when exploring what should be static or dynamic. The key is doing the analysis to understand what meets your use case the best now and into the future. Ask yourself and debate what changes may be necessary within the context of both the design system and the systems that may consume it. At a minimum, you’ll have made a conscious and thoughtful choice at the time when you built it.