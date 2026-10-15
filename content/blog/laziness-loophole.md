---
title: "The Laziness Loophole: How Human Shortcuts Become AI Autonomy"
date: 2026-10-14
slug: "laziness-loophole"
tags: ["ai", "leadership", "engineering"]
description: "AI is moving from answering to doing. The bigger risk isn't a rogue model. It's the human who stops reading."
draft: false
---

AI is moving from answering to doing. It used to draft your email. Now it can send it, negotiate your car, book your travel, and push your code.

When AI only produced text, a paragraph you didn't read cost you a bad email or a wrong fact. When AI takes action, the paragraph you didn't read can cost a lot more.

That's why the AI risk I worry about most isn't a rogue model. It's a tired human who stops reading.

We talk about "human in the loop" as if it were a safety feature you install once. It isn't. It's a behavior, and behaviors erode. People are busy, people are competitive, and people are, by default, a little lazy. I include myself in that.

My argument is simple. Every time a human skims instead of reads, clicks "approve" instead of checks, or removes a review step to ship faster, they hand a little more authority to the AI. No one decides to give it autonomy. It accumulates through shortcuts. I call this the laziness loophole.

![A person at a laptop presses an approve button while a long, unread scroll of text spills onto the floor; a dashed line leads to a wastebasket on fire.](/images/laziness-loophole.svg)

## The wall of text is already a consent form

You can see the loophole today in plain chat. Ask an AI for help and you often get a long, confident reply: a plan, some caveats, a few assumptions, and a quiet "I'll go ahead and…" buried in paragraph six.

Most people don't read all of it. They read the first line, see that it looks reasonable, and type "sounds good." That two-word reply now approves everything in the response, including the parts nobody read.

We've run this experiment before. In their study *The Biggest Lie on the Internet*, Jonathan Obar and Anne Oeldorf-Hirsch had 543 people sign up for a fake social network called NameDrop. 98% missed the clauses in its terms of service that shared their data with the NSA and their employers, and that asked for their first-born child as payment. Make something long enough and people will agree to it without reading it.

AI raises the stakes. When you skim a terms of service page, you agree to some rules. When you skim an AI's reply and say "sounds good," you might be telling it to go do something.

And the AI isn't being sneaky. The warning is usually right there in the reply. You just didn't read it, and your "sounds good" counts as a yes anyway.

## Agents are already doing the work

Car buying shows how fast this is moving. Collin Huntzinger, a 27-year-old first-time buyer in Keller, Texas, [used ChatGPT to negotiate a used 4Runner](https://dallasexpress.com/business-markets/can-ai-haggle-better-than-you-for-a-new-car/) with half a dozen dealers over text. It drafted his replies, decoded dealer tactics, and helped him get to $40,000 out the door with a $450 monthly payment instead of the $800 he was first offered.

The detail that matters: he didn't just paste whatever it wrote. He made ChatGPT explain each move so he understood the reasoning. That's a human in the loop doing the job.

That loop is shrinking. [Negoshify](https://www.slashgear.com/2161916/chatgpt-ai-car-buying-deal-negotiation/), an app that runs inside ChatGPT and Claude, can search dealer inventory, put a refundable $500 hold on a car, and negotiate for you. [CarEdge's agent](https://getcoai.com/?p=92036) contacts multiple dealers anonymously, and buyers can either review its approach or hand it full autonomy. Dealers are deploying AI on their side too. Soon it's agent versus agent, and the buyer who once read every text is glancing at the result between meetings. The deal still gets done, whether or not anyone actually understood it.

OpenAI launched [Dots](https://techradar.com/pro/openai-launches-dots-its-always-on-ai-agents-that-are-always-watching) on September 29, 2026: always-on agents that each get their own cloud computer and browser. You set a goal and boundaries, and the agent works out the next steps on its own, and keeps going after you close the app. Meta's Muse and a wave of startups are chasing the same "agent that manages your life" idea.

To their credit, these products ship with guardrails. Dots lets users write [Custom Rules](https://ascendants.in/industry_events/openai-dots-explained-how-it-works/) that allow some actions, require approval for others, or block them. Some actions, like changing a password or moving money, stay with the human.

But look at what every one of those guardrails depends on: a person who reads the approval request, writes thoughtful rules, and doesn't click "always allow" the third time they're interrupted. The guardrails only work if you're paying attention. But the whole pitch is that you don't have to.

## We're wired to win

Laziness isn't the only instinct at work. We're also built to compete. We want to get ahead, finish first, and win, and that drive is as human as cutting corners.

Put those two instincts together and the human in the loop is in trouble. The person who stops double-checking the agent's work ships more, looks more productive, and gets ahead. The person who reads every approval falls behind. Nobody has to decide to remove oversight. The incentives do it for them.

This isn't a new problem. In 1983, researcher Lisanne Bainbridge wrote a paper called "Ironies of Automation." Her point: the more a system does on its own, the more we count on a person to watch it, and people are bad at watching something that almost always works. She was writing about factories and cockpits. It fits a chat window just as well.

The pattern plays out at every level, from one engineer to a whole company. Approvals become batch approvals, then notifications, then a weekly log nobody opens. Each step feels like progress. Eventually the AI is acting on its own, and nobody ever actually decided to let it.

## Fake authorization, real consequences

This is where bad habits turn into real damage. Skim, auto-approve, or remove enough approvals and the AI is basically on its own. On paper, someone said yes. In reality, nobody was checking.

And it won't just be small stuff. An agent can email the wrong customer list, delete records it decided were duplicates, accept terms on a vendor site, spend budget, or push a change to production. Each of those can trace back to a "sounds good" someone typed without reading.

None of that needs an evil AI. It just needs an AI doing what it thought you asked, with nobody checking. Some mistakes will be minor. Some won't, and by the time anyone notices, it's already done.

Then comes the hard question: who is accountable? The human technically approved it. The AI technically had permission. Everyone followed the process, and the process failed.

## Two fixes: the product and the system

There are two places to close the loophole: the products we use, and the systems around the people using them.

**Fix the product.** Design can make real review easy and lazy approval harder:

- Keep approval requests short: what, where, how much, and how to undo it.
- Require a specific yes for anything you can't undo, like moving money, deleting data, messaging customers, or pushing to production. "Sounds good" to a long reply doesn't count.
- Flag rubber-stamping. Fifty approvals in two minutes means nobody is reviewing.

**Fix the system.** Design alone won't hold, because every safeguard can be skipped by someone in a hurry. The rest has to come from above the individual:

- Make someone clearly liable when an agent acts on an approval nobody read. Companies take review seriously when they're on the hook.
- Require audit trails that show who approved each action and what they actually saw.
- Reward checking. If speed is the only metric, review will lose.

Both slow things down a little. That's the point.

For leaders, the question isn't "do we have a human in the loop?" It's "what happens when that human stops reading?"

## The loophole is us

The story we tell about AI autonomy is usually about the machine taking control. The more likely story is quieter: we hand it over, one skipped paragraph and one auto-approve at a time.

AI doesn't have to get past us if we've already gotten out of the way. The next time an AI gives you a long answer and you're about to type "sounds good," ask yourself what you just agreed to.

## Sources

- [OpenAI launches Dots, its always-on AI agents](https://techradar.com/pro/openai-launches-dots-its-always-on-ai-agents-that-are-always-watching), TechRadar
- [What is ChatGPT Dots?](https://www.mindstudio.ai/blog/chatgpt-dots-explained), MindStudio
- [What is OpenAI Dots?](https://ascendants.in/industry_events/openai-dots-explained-how-it-works/), Ascendants
- [Can AI haggle better than you for a new car?](https://dallasexpress.com/business-markets/can-ai-haggle-better-than-you-for-a-new-car/), Dallas Express
- [Car buyers are turning to ChatGPT to help them get a better deal](https://www.slashgear.com/2161916/chatgpt-ai-car-buying-deal-negotiation/), SlashGear
- [AI agent negotiates car prices](https://getcoai.com/?p=92036), CO/AI
- [The Biggest Lie on the Internet](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2757465), Jonathan A. Obar and Anne Oeldorf-Hirsch
- Lisanne Bainbridge, "Ironies of Automation," *Automatica*, 1983
