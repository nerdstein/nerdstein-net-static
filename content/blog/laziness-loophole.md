---
title: "The Laziness Loophole: How Human Shortcuts Become AI Autonomy"
date: 2026-10-14
slug: "laziness-loophole"
tags: ["ai", "leadership", "engineering"]
description: "AI doesn't need to seize autonomy. We hand it over one skimmed reply and one auto-approve at a time."
draft: false
---

The AI risk I worry about most isn't a rogue model. It's a tired human who stops reading.

We talk about "human in the loop" as if it were a safety feature you install once. It isn't. It's a behavior, and behaviors erode. People are busy, people are competitive, and people are, by default, a little lazy. I include myself in that.

My argument is simple. Every time a human skims instead of reads, clicks "approve" instead of checks, or removes a review step to ship faster, they hand a little more authority to the AI. No one decides to give it autonomy. It accumulates through shortcuts. I call this the laziness loophole.

![A person at a laptop presses an approve button while a long, unread scroll of text spills onto the floor; a dashed line leads to a wastebasket on fire.](/images/laziness-loophole.svg)

## The wall of text is already a consent form

You can see the loophole today in plain chat. Ask an AI for help and you often get a long, confident reply: a plan, some caveats, a few assumptions, and a quiet "I'll go ahead and…" buried in paragraph six.

Most people don't read all of it. They read the first line, see that it looks reasonable, and type "sounds good." That two-word reply now approves everything in the response, including the parts nobody read.

We've run this experiment before. In their study *The Biggest Lie on the Internet*, Jonathan Obar and Anne Oeldorf-Hirsch had 543 people sign up for a fake social network called NameDrop. 98% missed the clauses in its terms of service that shared their data with the NSA and their employers, and that asked for their first-born child as payment. Length is a reliable way to get consent without understanding.

The difference is that a terms of service page is static. An AI's reply can describe actions it is about to take.

The problem isn't that the AI is hiding anything. Often the caveat is right there. The problem is that the approval is real and the review never happened.

## From answers to actions

When AI only produced text, an unread paragraph cost you a bad email or a wrong fact. Now AI is moving from answering to doing.

Car buying shows how fast this is moving. Collin Huntzinger, a 27-year-old first-time buyer in Keller, Texas, [used ChatGPT to negotiate a used 4Runner](https://dallasexpress.com/business-markets/can-ai-haggle-better-than-you-for-a-new-car/) with half a dozen dealers over text. It drafted his replies, decoded dealer tactics, and helped him get to $40,000 out the door with a $450 monthly payment instead of the $800 he was first offered.

The detail that matters: he didn't just paste whatever it wrote. He made ChatGPT explain each move so he understood the reasoning. That's a human in the loop doing the job.

That loop is shrinking. [Negoshify](https://www.slashgear.com/2161916/chatgpt-ai-car-buying-deal-negotiation/), an app that runs inside ChatGPT and Claude, can search dealer inventory, put a refundable $500 hold on a car, and negotiate for you. [CarEdge's agent](https://getcoai.com/?p=92036) contacts multiple dealers anonymously, and buyers can either review its approach or hand it full autonomy. Dealers are deploying AI on their side too. Soon it's agent versus agent, and the buyer who once read every text is glancing at the result between meetings. The deal still happens. Whether anyone understood it becomes optional.

OpenAI launched [Dots](https://techradar.com/pro/openai-launches-dots-its-always-on-ai-agents-that-are-always-watching) on September 29, 2026: always-on agents that each get their own cloud computer and browser. You set a goal and boundaries, and the agent works out the next steps on its own, and keeps going after you close the app. Meta's Muse and a wave of startups are chasing the same "agent that manages your life" idea.

To their credit, these products ship with guardrails. Dots lets users write [Custom Rules](https://ascendants.in/industry_events/openai-dots-explained-how-it-works/) that allow some actions, require approval for others, or block them. Some actions, like changing a password or moving money, stay with the human.

But look at what every one of those guardrails depends on: a person who reads the approval request, writes thoughtful rules, and doesn't click "always allow" the third time they're interrupted. The safety model assumes an attentive human. The product's selling point is that you don't have to be one.

## We're wired to win

Laziness isn't the only instinct at work. We're also built to compete. We want to get ahead, finish first, and win, and that drive is as human as cutting corners.

Put those two instincts together and the human in the loop is in trouble. The person who stops double-checking the agent's work ships more, looks more productive, and gets ahead. The person who reads every approval falls behind. Nobody has to decide to remove oversight. The incentives do it for them.

Lisanne Bainbridge saw a version of this coming in 1983. In "Ironies of Automation," she pointed out that the more we automate, the more we rely on humans to monitor the system, and humans are bad at sustained monitoring of something that almost always works. Forty years later, we're building the same setup with a chat window.

The pattern plays out at every level, from one engineer to a whole company. Approvals become batch approvals, then notifications, then a weekly log nobody opens. Each step feels like progress. The end state is an AI acting with authority no one explicitly granted, handed over by people doing what they're wired to do.

## Fake authorization, real consequences

This is where the loophole stops being about habits and starts being about outcomes. Once enough approvals are skimmed, auto-accepted, or removed, the AI is effectively running on its own. It has authorization on paper and none in practice.

That doesn't stay contained to small things. An agent can email the wrong customer list, delete records it decided were duplicates, accept terms on a vendor site, spend budget, or push a change to production. Each of those can trace back to a "sounds good" someone typed without reading.

None of that requires a malicious AI. It's an AI doing what it believed it was told, with consequences nobody intended and nobody reviewed. Some will be minor. Some will be significant, and by the time anyone notices, the action is done.

Then comes the hard question: who is accountable? The human technically approved it. The AI technically had permission. Everyone followed the process, and the process failed.

## Design helps. Systems decide.

Good product design can narrow the loophole. It can't close it, because it still relies on the same tired, competitive human. A few principles help at the margins:

- **Short asks for real decisions.** If an action needs approval, the request should fit on one screen: what, where, how much, and how to undo it. Burying an action in a long reply shouldn't count as asking.
- **"Sounds good" isn't blanket consent.** A two-word reply to a long message should approve only what was clearly listed, not everything mentioned.
- **Reversibility sets the bar.** Easily undone actions can run freely. Irreversible ones (money, deletion, external messages, production changes) need an explicit, specific yes every time.
- **Watch for rubber-stamping.** If someone approves 50 requests in two minutes, the system should notice that review has stopped and say so.
- **Loosening controls should be a decision.** Removing a human checkpoint should be a deliberate choice someone signs off on, not a setting someone toggled to stop the pop-ups.

Here's the uncomfortable part: none of that changes human nature. Every safeguard above can be skipped, toggled off, or rubber-stamped by someone in a hurry. If oversight depends on individual discipline, it will erode. That's not pessimism. It's how people work.

So the fix has to live above the individual, where skipping it isn't a personal choice:

- **Accountability that sticks.** Clear rules on who is liable when an agent acts on a fake approval: the company that deployed it, the vendor, or the person who clicked. Liability is what makes organizations care whether review is real.
- **Safe defaults by standard.** Irreversible actions like moving money, deleting data, or contacting customers should require verified human sign-off across products, the way seatbelts aren't an optional feature.
- **Audit trails by requirement.** Every agent action logged with who approved it and what they actually saw.
- **Incentives that reward checking.** Inside companies, slowing down to review has to count as performance, not friction. If speed is the only metric, oversight will lose.
- **Independent checks.** High-impact agent actions reviewed by a separate team or system with no stake in shipping faster.

None of these are free, and all of them slow things down a little. That's the point. Without them, the loophole is the default.

For leaders, the question isn't "do we have a human in the loop?" It's "what happens when that human stops reading?"

## The loophole is us

The story we tell about AI autonomy is usually about the machine taking control. The more likely story is quieter: we hand it over, one skipped paragraph and one auto-approve at a time.

AI doesn't need to get around the human if the human has already stepped aside. The next time an AI gives you a long answer and you're about to type "sounds good," ask yourself what you just agreed to.

## Sources

- [OpenAI launches Dots, its always-on AI agents](https://techradar.com/pro/openai-launches-dots-its-always-on-ai-agents-that-are-always-watching), TechRadar
- [What is ChatGPT Dots?](https://www.mindstudio.ai/blog/chatgpt-dots-explained), MindStudio
- [What is OpenAI Dots?](https://ascendants.in/industry_events/openai-dots-explained-how-it-works/), Ascendants
- [Can AI haggle better than you for a new car?](https://dallasexpress.com/business-markets/can-ai-haggle-better-than-you-for-a-new-car/), Dallas Express
- [Car buyers are turning to ChatGPT to help them get a better deal](https://www.slashgear.com/2161916/chatgpt-ai-car-buying-deal-negotiation/), SlashGear
- [AI agent negotiates car prices](https://getcoai.com/?p=92036), CO/AI
- [The Biggest Lie on the Internet](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2757465), Jonathan A. Obar and Anne Oeldorf-Hirsch
- Lisanne Bainbridge, "Ironies of Automation," *Automatica*, 1983
