---
title: "Imitation is the best form of flattery"
date: 2015-01-04
slug: "imitation-best-form-flattery"
tags: ["development", "drupal"]
description: "I personally believe cut-and-paste coding can be one of the sloppiest and least reliable ways of developing a product. Consider the source."
draft: false
---

I personally believe *cut-and-paste* coding can be one of the sloppiest and least reliable ways of developing a product. Consider the source.

 

After teaching Comp Sci for several years, I can confidently claim that this is the worst type of coding. Most of the cut-and-paste code comes from the web. Someone goes onto Stack Overflow, slaps in variables and values to meet their use case, and commits their change. Consider the source! You have no idea who posted the code, the merit of the code, or if it follows best practice. There is often a ton of metadata missing as well, e.g. the supported major/minor versions of the software, dependencies of the code, or full contextual code examples that leverage the posted snippet. I can say, it typically is not very good.

 

What is the merit of this code? It is simply for brainstorming and debugging. You may need ideas on how to develop something or examples on how to implement an API, etc. It is often best to look at several of these sources to consider and evaluate different approaches. The key point: the benefit of this source is far from just cut and paste. It requires more thought and consideration from your specific problem you are solving.

 

When could you consider a cut and paste strategy? *When the source is reliable*. 

 

One of my favorite things to do when developing a module in Drupal is to evaluate similar functionality in a core or widely-adopted contributed module. Core developers are often some of the brightest in the community. All code in core and the most popular contributed modules are highly scrutinized. Those who leverage Drupal daily often use the phrase, "Standing on the shoulder of giants". If you are copying code, this seems like the best place to get it. Identify a module that does something similar to what you are striving for and audit the code. 

 

As an example, I didn't know how to add a custom link to the configuration page in Drupal 8. (**Small plug**: *I am developing the Drupal 8 port of Password Policy.*) Drupal 8 uses an entirely new routing system, which handles the resolution of paths and callbacks in Drupal. I added a new path that started with the administrative configuration path, and it didn't work. So, I pulled up the User module in core, saw that it had an additional "links.menu.yml" file with similar information found in the "routing.yml" file. I copied some code, refactored it for my module/use case, and tested. Boom, winning.

 

*Imitation is the best form of flattery*. I'd rather imitate those that know what they are doing instead of an arbitrary website.