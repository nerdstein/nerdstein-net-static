---
title: "Thinking Out Loud, With Better Tools"
date: 2026-05-08
slug: "ai-assisted-blog-workflow"
tags: ["ai", "reflection", "personal", "engineering", "open-source"]
description: "Rebuilding this site with AI connects back to a lesson I learned the hard way as a new manager: communication is a skill, not a given."
draft: false
---

> "The single biggest problem in communication is the illusion that it has taken place." — George Bernard Shaw

When I was a newer manager, I was terrible at delegating. Not because I hoarded work — I genuinely wanted to hand things off. The problem was that what came out of my mouth and what existed in my head were two different things. I would give someone a task, they would execute what I described, and I would be surprised by the result. Every single time. It took me an embarrassingly long time to realize the gap was mine.

Clear communication, it turns out, is not a personality trait. It is a practiced skill. And like most skills, you have to fail at it repeatedly before you get any good.

## Ambiguity Is the Enemy, Not the Person

Delegation breaks down at the point of ambiguity. I think about this in terms of *degrees of freedom*: every gap in your communication is a degree of freedom you've handed to someone else. They will fill it in — not out of carelessness, but because they have to. They're trying to move forward. The problem is that their assumptions and your assumptions are almost never the same. The more ambiguous the instruction, the more degrees of freedom exist, and the further the outcome drifts from what you actually wanted. The failure mode is not that someone made a bad decision. The failure mode is that I created the conditions beyond my expectations.

In *Team of Teams*, Stanley McChrystal describes what it takes for a large organization to act with speed and coherence. His answer is not more command-and-control. It is shared consciousness — making sure that the people you trust to act independently actually understand *why*, not just *what*. The same principle applies to a one-on-one delegation conversation. The "why" is what makes the difference between someone executing a task and someone solving the right problem.

I got better at this over time, mostly through painful repetition. But now I have a different kind of collaborator helping me stay honest.

## AI as a Clarifying Mirror

One of the more useful things AI does for me is ask the question I forgot to ask myself. When I describe something imprecisely — in a prompt, in a spec, in a rough outline for a blog post — a good AI interaction surfaces the ambiguity instead of smoothing over it. It responds to what I actually said, not what I meant. That is sometimes uncomfortable. It is also exactly what a good colleague does.

I've started using this for writing in a way I didn't anticipate. I have no shortage of opinions and half-formed ideas. What I've historically lacked is time — time to shape a rough thought into something coherent enough to be worth reading. With AI in the loop, I can hand over notes that are genuinely messy and get back something that sounds like me, just more organized. The voice stays mine. The structure gets help.

{{< callout >}}
This post, for instance, started as a few paragraphs of stream-of-consciousness notes. AI helped me find the shape. I rewrote the parts that didn't sound right. That feels like the right division of labor.
{{< /callout >}}

I want to be clear about what I think this is and isn't. It is not ghostwriting — the ideas, the opinions, and the edits are mine. It is closer to having a very patient editor who is available at 11pm and never charges by the hour. The goal is a better version of what I already wanted to say, not a substitute for having something to say.

## The Infrastructure Problem Was Real Too

There is a more practical layer to this story. My old blog ran on Drupal — naturally — and for years that was fine. I was deep in the community, I knew the platform, and maintaining it was almost second nature. Then life got busier. The site fell behind on updates. Writing took a back seat to everything else demanding my attention.

Eventually the friction of maintaining a dynamic CMS just to publish occasional blog posts stopped making sense. So I rebuilt the whole thing using AI as the primary engineering collaborator. What came out the other side is a Hugo-based static site, hosted on Cloudflare Pages, content managed through a straightforward GitOps workflow. The total hosting cost is zero. Deployments happen automatically on `git push`. The whole migration — extracting 116 posts from the old site and converting them to Markdown — took a few hours, not weeks.

It is genuinely impressive what you can build in an afternoon now if you know how to ask the right questions. The barrier to entry for "just ship it" has collapsed.

## A Simpler Tool for What Actually Matters

I didn't rebuild this site because I needed a new hobby project. I rebuilt it because I want to write again, and the old setup had become an obstacle. The new one gets out of the way.

What I hope to do with it is share things I'm actually learning — mostly about AI and how it's changing the way I work, lead, and think about software. There is a lot of noise in that space right now and not enough people saying "here is what I actually tried and what actually happened." I want to be one of those people.

The question I keep coming back to: if AI makes it easier to communicate clearly, does that make us better thinkers, or just better at disguising muddled ones? I don't have a clean answer yet. But I'd rather work through it out loud than wait until I do.
