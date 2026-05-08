---
title: "Finally! A website refresh"
date: 2020-12-28
slug: "new-site-2020"
tags: ["development", "drupal", "people"]
description: "Let me welcome you to the new nerdstein.net. I'd like to thank Ana Laura Coto for help with the design."
draft: false
---

Let me welcome you to the new nerdstein.net. I'd like to thank Ana Laura Coto for help with the design. I'd like also thank Jonathan Daggerhart for being there when I needed an assist. I am really happy to finally share this project with the world.

This has been a long time coming. Three years. Yes, you read that correctly. Three years. Why? I prioritized learning. And, I am slow and methodical. This website is a culmination of many things I learned over a three year span.

But, three years?!? Yep. I have a rewarding and challenging full time job at Acquia. I have a family with two young kids. This project was all done in my spare time and at my convenience. Most of my time and learning is invested in SimplyTest.me. But, this project gave me a high degree of freedom on my own timeline. I wanted to learn things well and understand things properly. I did it piece by piece. Drupal evolved a lot in three years, as well. There was a lot to learn. And, then 2020 happened (I'll hopefully blog more on that soon).

For the rest of this blog post, I'd like to reflect on these efforts and learning.

## From Drupal 7 to Drupal 8 and then Drupal 9

Drupal evolved significantly from Drupal 7 to Drupal 9. My original goal was to launch this with Drupal 8. Then life happened. Then Drupal rolled more features and made it even easier and better to launch my site. I'll share some specifics below. Regardless, Drupal has established itself as a great tool for progressive enhancements.

One notable change on this journey is how the community adopted Composer. I recall the very basic support when Drupal 8 was launched. Major changes were made when I upgraded the site to Drupal 8.7, which totally revamped the Composer work. I did the same when Drupal 9 came out. The community made some significant progress, but I'd love to see this stabilize now. I made heavy use of Composer and it's DevOps capabilities to script some of the integrations with my design system. This area of work was not well documented, especially in moving between versions and resolving issues.

## New server

I was long overdue for a tech refresh. I had the same VPS running my Drupal 7 site for over seven years. It served me well. I spun up a VPS for a few Drupal 8 sites I hosted for local non-profit orgs that couldn't afford it. My Drupal 8 development site ran there for several years. The non-profits moved on due to grant funding and poor technical support (hint: if you can't do something well, don't do it). And, that Drupal 8 server rapidly dated itself.

I was able to shut down both VPS servers and create a brand new Ubuntu 20.04 on Linode. Linode has been a sponsor of SimplyTest.me, helping offset the cost of it's development infrastructure. I'd hardly call the experience of Ubuntu 20.04 learning; it was a breeze setting up a Drupal 9 environment. These systems have come a long way even in seven years. Shutting down the VPS servers is bittersweet. I've removed some significant tech debt but those servers were rock solid. No regerts.

## Design Systems and Drupal Integrations

The biggest emphasis of learning was the front-end work of the design system. I am still so far from an expert. But, I definitely understand it now. I started with Pattern Lab. I broke down Ana Laura's design into a series of atomic components. I developed them. I learned more about SCSS and building of front-end assets. I mocked up these patterns with JSON data objects and finally built out representative pages with the pattern.

Once the design system was done, I started on the Drupal integration. My goal was to pull as much as possible from the design system (no cheating!). Composer made it easy for me to keep the design system and theme separated. I leveraged the Components module and proceeded to site build and theme simultaneously. Some of this was challenging. It was a fight between properly structuring content, overriding Twig themes, leveraging the Components module to include pattern markup, and parsing Drupal-related data objects.

I blogged about this several times, both in terms of the concepts I used and the architecture I leveraged. Please feel free to read more about this if you are interested.

## Twig. All the Twig.

Developing Twig was hands-down the most time consuming part of this project unquestionably. I spent countless hours digging through Drupal rendered objects, raw data, attributes of that data, and much more. I tweaked the display settings, created new view modes, did more tweaks, changed more Twig, and this went on endlessly. Data objects passed to Twig were massive and nearly impossible to debug without printing keys, refreshing, and traversing deeply nested objects. The syntax changed with every different entity and then even more with Views. Yes, Drupal is incredibly powerful and extensible. But, I continue to be surprised by the developer experience around Twig. I just wish this was simpler. I know the community has developed several utility modules. I need to dig into those more.

## Media System: image links

I had aspirations of contributing a composite field type module back to Drupal core. Developing this module, which never got complete, was a huge rabbit hole. I thought it would be relatively straight forward to inherit the core-provided image and link field types into one new field type. This was significantly more complex, especially when dealing with cardinality, managing data storage/schemas, and dealing with field widgets that were built atomically. This approach was rapidly becoming complex and it didn't seem like it needed to be. Then, help was on the way...

Daggerhart shared with me the new Media entity delivered as part of the Media system in Drupal 8. I was able to create an Image Link media type that was composed of an image field and a link field. This was super easy. From this, I got all of the expected benefits: Views support, easy integration with other entities, and the perks of the new media features in Drupal. Lesson learned: spend some time figuring out what parts of Drupal can be used before diving into code.

## Migration from Drupal 7

My website is quite simple. It's a basic blog. I wanted a simple way to migrate the content. Drupal offered that with it's native Drupal to Drupal migrate UI.

Set up was simple. I was able to set up a secondary database within settings.php for my Drupal 7 database. I archived to the files directory on Drupal 7, extracted them in a specific file path, and entered that path in the UI.

When I ran it, I got a nice confirmation page of potential issues with the Drupal 7 configuration, modules, and structure. I worked through it, ran the migration, and it basically worked. I had a few nodes that did not properly map their type. I cleaned this up through the database by manually editing the node type in the node and node revisions tables, followed up with a cache clear. I also had a few nodes that did not display the body field content. I simply re-saved the node and it worked.

I had to run this migration multiple times over three years as I refreshed the content on my current site. The UI didn't offer a rollback (this would be a nice feature through the UI) and had a big red note of caution when running multiple migrations. I did it anyways and it seemed to work fine for me (again, with my simple use case). Buyer beware.

To learn what happened behind the scenes, I audited all of the migration classes and configuration that were created. Kudos to those who worked on making the migration experience a positive one. I was really surprised how much was automated, how insightful it was, how smooth it went, and how easy it would have been to override the underlying config it created.

## TugboatQA

As I previously shared, I wanted a tech refresh. I thought about spinning up a development server, but this isn't really a modern CI/CD workflow. Having such a positive experience with TugboatQA on SimplyTest.me, I wanted to rapidly see changes before posting them live. And, I wanted something that didn't require me to mess around with another server. TugboatQA for the win.

Set up was straightforward. This may be potentially because I understood most of the concepts from SimplyTest.me, even though the use case couldn't be more different for my personal website. I followed the documentation and configured it within a few hours (love their IaC set up). I actually found a bug in how I implemented Composer paths, which I subsequently fixed.

## Ported Block Type Templates module to Drupal 9

Again, I spend a lot of my personal time on SimplyTest.me. I still moonlight with some module maintenance, but I do a pretty poor job at this if I am being honest. I did use the Block Type Templates module I developed to have more fine grain control of block Twig. This was immensely helpful with the design system integration. But, I had to port it to Drupal 9. I also cleaned up the issue queue and added some nice features. I hope this helps others, too.

## Future Goals

This website is definitely not done. I have some open issues I've logged. I need to clean up some content, fix even more styling, and finish the Tugboat implementation now that I've launched. It's done enough for me to not maintain two websites any longer. Please feel free to let me know if you find any issues.

I also want to add more DevOps. When a PR gets merged, I want to set up a GitHub action to trigger the deployment on prod: pull updates from Git, load the config, run the database updates, and clear the cache. My confidence is a lot higher with Tugboat and my CI/CD workflow in the mix. This should be fun.

I'll be finally adding SSL support for my site, but I'd like to do this by learning more about the edge layer. I need more research but leaning towards using CloudFlare for this.

Pattern Lab has evolved majorly since I first set up the design system. I'll be upgrading this with time and I have the Drupal integration versioned to allow for changes like this to be done in the future.

## Final Thoughts

I'm glad to finally be able to launch this thing. I learned a lot doing this. Drupal is still a fantastic option for digital experiences. It does so much. Drupal 9 brings all of the previous years of learnings, new features, great performance, modernized dev workflows, and continues to deliver a highly extensible framework. I thought a lot about developing this in something like Gatsby, but would have still wanted a FOSS backend like Drupal. It did everything I needed natively.