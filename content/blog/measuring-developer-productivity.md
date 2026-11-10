---
title: "Engineering Fought Productivity Metrics. AI Ended the Fight."
date: 2026-11-09
slug: "measuring-developer-productivity"
tags: ["ai", "engineering", "leadership"]
description: "AI put a new, fast-growing line item on engineering's budget. No single metric can tell you if it's paying off. Attribution and optimization can."
draft: false
---

Uber spent its entire 2026 AI token budget in four months. Salesforce's Anthropic bill is reportedly running around $300 million a year. Meta employees built an internal leaderboard that ranked roughly 85,000 people by token consumption and logged more than 60 trillion tokens in a single month.

Then someone asked the obvious question: what did we get for it?

Uber's COO, Andrew Macdonald, [put it plainly](https://fortune.com/2026/05/28/tokenmaxxing-is-dead-companies-didnt-get-the-roi-from-ai-they-wanted-to-see/): "If you're not actually able to draw a line to how much useful features and functionality you're shipping to your users, [the token costs are] harder to justify."

Most engineering organizations can't draw that line today. That's the problem I want to work through.

![A car dashboard: the speedometer needle is pegged in the red, the gauge marked with a bug is also in the red, and the gauge marked with a coin is nearly empty, with a warning light glowing between them.](/images/acceleration-whiplash.svg)

## Engineering lost its exemption

For a long time, software engineering got a pass on hard productivity measurement. When McKinsey published "Yes, you can measure software developer productivity" in 2023, the industry pushed back hard. Kent Beck called it "so absurd and naive that it makes no sense to critique it in detail," and he and Gergely Orosz [wrote a two-part rebuttal](https://newsletter.pragmaticengineer.com/p/measuring-developer-productivity) arguing it would do more harm than good.

On the method, they were right. Measuring individual effort and output invites gaming. But the argument for leaving engineering alone depended on its costs being mostly headcount, a number finance already understood.

AI changed that. Token spend is new, variable, and growing fast. It shows up on a bill every month, and finance wants to know what it bought. In June 2026, the Linux Foundation [launched the Tokenomics Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-intent-to-launch-the-tokenomics-foundation-to-establish-open-standards-for-ai-cost-management) to standardize how companies measure AI spend, with Google Cloud, Microsoft, JPMorganChase, and Salesforce among its backers. The FinOps Foundation's framing: "Token costs and efficiency have become a CEO-level concern."

Engineering is no longer exempt from measurement. The question is whether we measure it well or let someone else measure it badly.

## There is still no single metric

People want a simple answer. Is AI working? Yes or no. Give me the number.

There isn't one, and DORA and SPACE explained why years ago. DORA balanced speed (deployment frequency, lead time) against stability (change failure rate, recovery time). SPACE went wider and added satisfaction, collaboration, and flow. Both made the same point: productivity spans the whole software development lifecycle, and pushing on one measure moves the others.

AI has proven them right. The [2025 DORA report](https://dora.dev/insights/balancing-ai-tensions/) found that higher AI adoption goes with higher delivery throughput and higher instability at the same time. Faros calls this the acceleration whiplash. Their [2026 report](https://www.faros.ai/blog/ai-acceleration-whiplash-takeaways), built on telemetry from 22,000 developers, found individual output rising sharply while bugs per developer rose 54% and incidents per pull request rose 242.7%.

The work also piles up in review. In Faros's [2025 data](https://www.faros.ai/blog/ai-productivity-paradox-report-2025), developers on high-adoption teams merged 98% more pull requests, but those pull requests were 154% larger and review time rose 91%. In their 2026 data, review time was up 441%. Eliyahu Goldratt made this point in *The Goal*: speeding up a step that isn't the constraint doesn't make the system faster. It just builds a bigger pile in front of the constraint. AI sped up writing code. Review became the constraint.

Asking developers doesn't settle it either. Yegor Denisov-Blanch's research group at Stanford has studied close to 100,000 developers across more than 600 companies. [They found](https://getcoai.com/video/does-ai-actually-boost-developer-productivity-100k-devs-study-yegor-denisov-blanch-stanford/) a net productivity gain of 15–20% once rework is counted, and that asking developers how productive they feel is barely better than a coin flip.

If you only looked at pull requests merged, or only asked your team, you'd call this a win. That's why DORA and SPACE still matter. They make you look at everything at once.

## Good teams get great, bad teams get worse, faster

DORA's sharpest finding is that AI is an amplifier. It makes good teams great and bad teams worse, faster. A team with strong testing, small batches, and fast review turns AI output into shipped value. A team without those things turns it into incidents.

I believe that. But it isn't useful until you can say which kind of team you are, with numbers.

The research is starting to provide them. In an [August 2026 study](https://arxiv.org/abs/2608.25241), Denisov-Blanch and colleagues at Stanford and Carnegie Mellon looked at 441 repositories adopting coding agents. Every group got faster, with 28–38% more commits. But repositories without committed AI configuration, the `AGENTS.md` and `CLAUDE.md` files that tell an agent how a codebase works, saw code complexity rise about twice as much (53% versus 27%) and static-analysis warnings rise 1.7 times more. Same tools, same speedup, very different codebases. And 73.8% of those configuration files were committed once and never touched again.

That's the amplifier, measured. The teams that wrote down how their system works got the speed without as much of the mess.

## DORA is starting to price it in

DORA and SPACE were built to measure software delivery as a discipline. They didn't connect delivery to the business or to money. The [DX Core 4](https://getdx.com/research/measuring-developer-productivity-with-the-dx-core-4/) added a business impact dimension, and now DORA itself is moving.

In May 2026, Google Cloud's DORA team, led by Nathen Harvey, published [The ROI of AI-Assisted Software Development](https://www.infoq.com/news/2026/05/dora-roi-ai-assisted-dev-report/). It puts dollars on the tradeoffs. Adoption follows a J-curve, with a productivity dip before the payoff. Reviewing AI-generated code carries a **verification tax**. Instability carries an **instability tax**: in their sample model, a change failure rate moving from 5% to 6% costs $344,000 in downtime. Their summary is the best one-line version of this whole argument I've seen: "We don't measure AI by the code it writes but by the bottlenecks it clears."

This is the right direction. DORA is adding the business and financial layers that were missing. But an ROI model is a planning tool. It tells you what to expect. It can't tell you what actually happened in your organization last quarter. For that, you need your own data.

## Attribution: from token to outcome

The first fix is attribution. You need to be able to trace AI activity to the work it produced, and that work to an outcome someone cares about.

Volume alone won't do it. A [Microsoft study](https://arxiv.org/abs/2607.01418) of tens of thousands of engineers adopting Claude Code and GitHub Copilot CLI found adopters merged roughly 24% more pull requests. The authors were careful to add that "a merged PR is not the same as the value it delivers."

The chain from token to value looks like this: an AI session produces a change, the change merges into a pull request, the pull request ships a feature or fixes an incident, and the feature moves a business measure. Each link needs data. Most organizations have the first link (a usage dashboard) and the last link (business metrics), and nothing connecting them.

{{< callout >}}
If you can't tell AI-written code from human-written code, you're mostly guessing at AI's return.
{{< /callout >}}

Once the links exist, better metrics become possible. **Cost per merged pull request** divides AI spend by the work that actually shipped. One analysis [compared two agents](https://larridin.com/measurement-guide/agent-effectiveness/cost-per-outcome/) at the same adoption rate costing $29.62 and $10.97 per merged pull request. That's a tool decision you can actually make.

This isn't a new idea, just a new input. Amazon already measures software this way. Its **Cost to Serve Software** metric, adapted from the retail Cost to Serve metric Andy Jassy has highlighted in Amazon's shareholder letters, divides the total cost of delivering software by the units delivered: deployments for services, completed pull requests for monoliths and mobile apps. Jim Haughwout, Amazon's VP of Software Builder Experience, [reported](https://aws.amazon.com/blogs/enterprise-strategy/business-value-of-developer-experience-improvements-amazons-15-9-breakthrough) a 15.9% year-over-year drop in that cost in 2024. Token spend belongs in the same numerator as salaries and infrastructure. Once it's there, AI has to lower the cost per unit of software that reaches customers, not just raise the number of units.

Cost is one lens. It tells you what a unit of software costs, but not how much human effort went into getting the AI's output there. **Autonomy rate** is another lens: the share of AI-generated pull requests that ship without a human rewrite. A high rate means agents are doing work. A low rate means they're creating it, and someone is quietly paying for that rework. Put cost and autonomy next to change failure rate and you can see whether cheap output is turning into expensive incidents.

This is also how you quantify the amplifier for your own teams. If a team's cost per merged pull request falls while its change failure rate holds steady, it's getting better. If its throughput rises while incidents rise faster, it's getting worse, faster.

## From maxxing to optimizing

The second fix is to stop rewarding consumption. Tokenmaxxing, ranking people by how many tokens they burn, is the lines-of-code mistake again. Amazon's "Kirorank" leaderboard was [reportedly shut down](https://www.hcamag.com/us/specialization/transformation/amazon-workers-are-gaming-the-ai-leaderboard-hr-built-it/575083) after employees invented meaningless tasks to raise their counts. That's Goodhart's law: when a measure becomes a target, it stops being a good measure.

The overcorrection is just as bad. Hard token caps punish the people getting the most value. As I wrote in [Wave Three](/blog/wave-three-ai-development), capping spend arbitrarily is the wrong control. Faros CEO Vitaly Gordon [frames it well](https://www.faros.ai/blog/from-token-maxxing-to-outcome-maxxing): "You need to know whether your team's token spend is too high — or not high enough." His example is an engineer who spent $20,000 on tokens in one month. Without attribution, nobody knew whether to restrict that person or promote them.

The FinOps Foundation offers a better target than raw consumption. J.R. Storment [defines](https://finops.org/insights/token-economics-the-atomic-unit-of-ai-value/) **token yield rate** as "the share of generated tokens that contributed to a downstream business action, after accounting for retries, abandoned sessions, and outputs that failed quality review." That's a number worth raising. Total tokens isn't.

Optimizing means using attribution data to change behavior:

- **Model routing.** Not every task needs the most expensive model. Send boilerplate and simple fixes to cheaper models, and save frontier models for work where your own data shows they earn their cost.
- **Analyzing AI activity.** Look at which workflows, prompts, and agents produce merged, stable work, and which produce retries and churn. Spread what works and drop what doesn't.
- **Maintaining the context.** The Stanford and Carnegie Mellon data says committed AI configuration roughly halves the complexity cost of adopting agents. Treat those files like code: review them, and update them as the system changes.
- **Investing in the constraint.** If review is where the work piles up, spend there: smaller changes, better automated tests, AI-assisted review with a human making the final call.

None of this is a cost-cutting exercise. The goal is to get more of the outcomes you want for each dollar spent.

## The fundamentals didn't change

AI is a new capability, not a new definition of good engineering. Speed, quality, security, stability, and developer experience still matter, and they still trade off against each other. DORA and SPACE are still the right foundation, and DORA's newest work is extending that foundation toward the business and the budget.

What changed is that engineering now has a cost the business can see, and it expects an answer. The organizations that can trace AI activity to business outcomes will know where to invest. The rest will keep arguing about leaderboards.

So, can you draw the line from your AI spend to something your customers noticed?
