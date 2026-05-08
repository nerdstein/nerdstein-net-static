---
title: "Exploring simplicity in Drupal design components"
date: 2017-10-02
slug: "exploring-simplicity-drupal-design-components"
tags: ["development", "drupal", "people"]
description: "Component-based architectures have become both a popular and fairly crowded space in the Drupal community."
draft: false
---

Component-based architectures have become both a popular and fairly crowded space in the Drupal community. For over a year, I have followed the progress of some tools created by those leveraging Pattern Lab as a component based design library. I can’t claim to know the full breadth of problems these individuals encountered, many of which are experienced technologists in our space. But, every solution I have seen has been complex and demonstrates some architectural red flags. I wanted to take a fresh look. I paid a designer to redesign my blog for a migration to Drupal 8. This presented the perfect opportunity to try this out. Consider the following post a simple approach you might be able to use.

 

I set out to explore this space independently based on my intuition that this seemed overly complex and didn’t need to be. I wanted an approach that was both a simple integration and completely decoupled, as I believe any design library should be capable of being reused throughout any enterprise of digital properties. This means not packaging Pattern Lab with a specific Drupal theme. This separation also helps with a separation of duties and defined collaboration between a creative team and a technical team. I respect and wanted to preserve the conventional model of a visual experience driving the technology. Architecturally, I wanted the creative artifacts to be reused directly by Drupal (as much as possible) to afford ongoing parity with proposed design changes. The rest of this blog post articulates my approach and findings.

 

First, let’s start with Pattern Lab. While I received an HTML prototype from the designer, I actually believe Pattern Lab eliminates the need for conventional prototyping. The design library, specifically the “pages” aspect of atomic design, effectively replaces a conventional prototype. While my exercise was converting what the designer turned over to me, I believe it to be perfectly reasonable for Pattern Lab to assume this responsibility both as a prototyping tool and a living design library routinely updated as one.

 

I [created a GitHub repo](https://github.com/nerdstein/nerdstein-design-library) to house all of my creative assets. Deliberately, I documented everything I learned and my approach within the readme.md file. This not only helped me in jumping back into this amongst context switching, it also reads like a series of learnings from my exploration. While it’s not complete, this repo continues to be updated based on my progress.

 

Logically, I selected a Twig and PHP-based Pattern Lab in line with my own comfort level and integration with Drupal. The PHP aspect was just preference but was needed for Twig to properly work (note: they also offer a Node-based Pattern Lab). I can see how this selection could become a potential limitation for an enterprise that may contain applications not tied to Twig or PHP. People could explore converting Twig to other frameworks for extended integration across other digital frameworks. There may even be tools out there that perform these conversions automatically. That could be part of a compilation process I describe below, where a Twig file is the source of truth and a set of additional template files of various formats are produced.

 

For my Pattern Lab implementation, I observed the standard atoms, molecules, organisms, and pages described in Brad Frost’s [Atomic Design](http://bradfrost.com/blog/post/atomic-design-book/) book. And, basically, I began splicing the prototype into these patterns. I leveraged [GitHub issues](https://github.com/nerdstein/nerdstein-design-library/issues) to define how I wanted it to be spliced, affording opportunities for anyone else to pitch in if they wanted to play around. Once all of the issues are completed, the prototype will be deprecated and removed from the repo altogether.

 

Each pattern maintains pattern-specific files for SCSS, Twig, JSON for design level variations, and a markdown file for documentation ([example](https://github.com/nerdstein/nerdstein-design-library/tree/master/design-library/source/_patterns/01-atoms/01-list-title)). This architecture allows each pattern to be self contained. I created a [Gulpfile](https://github.com/nerdstein/nerdstein-design-library/blob/master/design-library/gulpfile.js) to write a set of commands that compile and aggregate the SCSS into one primary CSS file. While this is not necessary, this simplified both the Pattern Lab implementation and the integration to Drupal ([basically just including one CSS file in a theme](https://github.com/nerdstein/nerdstein-drupal8/blob/master/code/drupal/web/themes/nerdstein/nerdstein.libraries.yml#L5)).

 

One key concept for an integrated and collaborative Pattern Lab is around change management. First, I chose to use [releases](https://github.com/nerdstein/nerdstein-design-library/releases) to pin the design library at a specific tag when performing the integration. This affords me control to release design changes to Drupal after properly staging them and addressing any issues that arise. This would be especially important if existing patterns are removed or the attributes change. While I have not done this yet, I plan to articulate design library changes within release notes. Next, I leveraged Pattern Lab’s native [exporting feature](http://patternlab.io/docs/advanced-exporting-patterns.html) to generate HTML used for reviewing design changes within pull requests. Pattern Lab creates HTML for every pattern, but I have found the page patterns to be the most useful to review changes with broader context for pattern interactivity and common use. Change management instructions are captured within the [pull request template](https://github.com/nerdstein/nerdstein-design-library/blob/master/.github/PULL_REQUEST_TEMPLATE.md), respecting forks and branches, and leveraging Github’s HTML Preview tool to [preview pages](http://htmlpreview.github.io/?https://github.com/nerdstein/nerdstein-design-library/blob/master/html/patterns/04-pages-01-sidebar-sidebar/04-pages-01-sidebar-sidebar.html). This architecture allows me to review every change that comes in. And, again, this full process is captured in the [readme](https://github.com/nerdstein/nerdstein-design-library/blob/master/readme.md).

 

For Drupal, the result is one CSS file, a set of Twig files per pattern, and all of this is done before Drupal is even considered. There are other considerations, like images and JavaScript files, that must certainly be considered but observe similar integration approaches.

 

Integrating Pattern Lab with Drupal 8 was surprisingly painless. Drupal 8 ships with Composer. I was able to reference the Pattern Lab [GitHub repo](https://github.com/nerdstein/nerdstein-drupal8/blob/master/code/drupal/composer.json#L19) in Drupal’s Composer.json, [specify the version](https://github.com/nerdstein/nerdstein-drupal8/blob/master/code/drupal/composer.json#L34) of the design library I wanted, and run Composer update to get the code. I also added a [Composer.json file](https://github.com/nerdstein/nerdstein-design-library/blob/master/composer.json) to the Pattern Lab repo for all of the proper metadata.

 

Next, I needed to wire in the CSS. This was a simple one line added to the theme [library.yml file](https://github.com/nerdstein/nerdstein-drupal8/blob/master/code/drupal/web/themes/nerdstein/nerdstein.libraries.yml#L5). This leveraged a relative path, which ends up being cached by the theme system in Drupal.

 

Lastly, I needed to be able to get access to the Twig files. I leveraged the Components module in Drupal 8 and added the Twig namespaces for atoms, molecules, and organisms into the [info.yml file](https://github.com/nerdstein/nerdstein-drupal8/blob/master/code/drupal/web/themes/nerdstein/nerdstein.info.yml#L19). Pages would be built by Drupal and were not necessary. Arguably, this is the least sexy part of the integration, as each pattern needs to be registered. I tried to find a way to do this recursively but it introduced issues between how Pattern Lab included other patterns within Twig.

 

 

 

Once this was complete, the Drupal site building commenced. I set up a series of content types, taxonomies, Views, and custom block types. I installed the Block Type Templates module to have Twig suggestions per Block Type. I proceeded to create or override the Twig files in Drupal. This was trivially simple with the Components module ([example](https://github.com/nerdstein/nerdstein-drupal8/blob/master/code/drupal/web/themes/nerdstein/templates/block--block-content-section.html.twig)). I routinely included Pattern Lab Twig files, mapped them to their respective Drupal attributes, and it worked flawlessly. There was very little additional CSS or markup needed for me to do.

 

Of note, I ended up enhancing and tweaking the Pattern Lab patterns as part of the site building process. One example was the alt text of an image. Drupal had this and I unintentionally left it out of one of the patterns. While my approach may have suggested this was a clean separation from creative to design, I ended up making some adjustments and enhancements when performing implementation.

 

I’m sure there are many edge cases that my simple integration does not cover. But, I’m pretty confident that such an approach covers common use cases. I managed to build global and contextual page elements with standard core-sponsored tools (custom block types, Views, content types, etc). Such an architecture affords clean integration with Panels, Place Block, Settings Tray, and many other well established Drupal approaches. Of note, I was anticipating needing to install something like Paragraphs but there was very little I couldn’t accomplish without Core. And, quite frankly, introducing any additional complexity to this integration should be carefully evaluated based on need.

 

I welcome your feedback on this approach. I’d love to hear of additional problems this does not cover. If you want to explore this further, please feel free to contribute or review the code repos noted above.