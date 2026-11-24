---
title: "The Patch Window Closed. Now What?"
date: 2026-11-24
slug: "patch-window-closed"
tags: ["engineering", "ai", "agile"]
description: "AI changed the odds in security. Attackers move in minutes, and defenders need to rethink where they place their risk."
draft: false
---

On October 14, Microsoft [patched 1,413 vulnerabilities](https://thehackernews.com/2026/10/microsoft-patches-record-1413-flaws.html) in a single Patch Tuesday, a record. This month brought another 1,252, and in the same week, attackers were exploiting critical flaws in [Cisco Expressway and VMware vCenter](https://thehackernews.com/2026/11/hackers-exploit-critical-vmware-cisco.html). The vCenter bug had been exploited for two months before a patch existed.

Security is rarely a choice between risk and no risk. It's a juggling act: how likely something is, how much it would hurt the business, and how much of that you're comfortable carrying. Every organization has already placed its bets, usually without saying so. A 30-day SLA for critical vulnerabilities is a bet that attackers won't get there first. A patch held through a holiday code freeze is a bet that a broken deploy is the bigger danger.

Those bets were placed for a slower world. AI changed the odds, and most organizations haven't moved their bets to match.

## The problem: the odds changed

### Attacks are outrunning patch cycles

Google's Threat Intelligence Group [found](https://www.csoonline.com/article/4230247/ai-accelerates-n-day-attacks-as-flaw-disclosures-and-exploits-double.html) that monthly CVE disclosures doubled between January and August 2026, to more than 10,700. That's roughly 350 new vulnerabilities a day. In June, CISA [cut the federal deadline](https://www.bleepingcomputer.com/news/security/cisa-tells-govt-agencies-to-patch-critical-exploited-flaws-in-3-days/amp) for fixing the highest-risk exploited flaws from roughly 21 days to three.

Three days won't last. Microsoft's latest Digital Defense Report [puts](https://blog.barracuda.com/2026/10/28/ai-cybersecurity-threats--microsoft-report-findings) the median time from discovery to weaponization well under 24 hours. In September, an AI agent [broke into the Dutch Institute for Vulnerability Disclosure](https://bleepingcomputer.com/news/security/divd-says-zammad-zero-days-enabled-ai-driven-network-breach) by chaining two zero-days in its helpdesk software, going from first access to root in 12 minutes without waiting on a human. The gap between finding a flaw and exploiting it is heading toward minutes.

### Attackers have the same models

Defenders got frontier security models first, but the head start is short. Anthropic, which runs Project Glasswing, [expects](https://www.anthropic.com/research/expanding-project-glasswing) that "within 6 to 12 months... many other AI companies will have Mythos-class models," some without the same safeguards. Open-weight models are already closing the gap, and anyone can run those.

The attacks are already here. In October, CrowdStrike tracked a China-nexus group [running AI agents against more than 200 organizations](https://bleepingcomputer.com/news/security/chinese-hackers-use-artex-ai-in-automated-attacks-against-200-orgs) in 11 days, with humans stepping in only at decision points. The operators told the agents to skip machines running CrowdStrike's endpoint protection. They didn't need to beat strong defenses. There were plenty of weak ones. Exploited zero-days, which held at 8 to 12 a month through mid-2026, [jumped to 22](https://cloud.google.com/blog/topics/threat-intelligence/vulnerability-discovery-and-exploitation-trends-in-the-ai-era) in August.

### People can't review it all by hand

Glasswing found more than 10,000 high- or critical-severity flaws with its first partners in a matter of weeks. Anthropic's conclusion: "the bottleneck in cybersecurity is now verifying, disclosing, and patching the large numbers of vulnerabilities that Mythos-class models can surface."

Most security teams still evaluate findings by hand: read the report, reproduce it, judge the severity, decide whether it's real. That worked when findings arrived by the dozen. It doesn't work at 350 new CVEs a day, plus whatever your own scanners turn up. Attackers automated their side. Most defenders haven't.

## What to do about it: move the risk

Shipping a fix quickly carries risk, because it might break something. Waiting carries risk, because someone might exploit the flaw first. For years, most organizations put their risk on waiting. That's no longer the safe bet.

The work now is to make shipping fast the safer option. That takes the DevOps practices we already know, AI agents to take manual work off people's plates, and the business behind it. In a [Sygnia survey](https://thehackernews.com/2026/07/73-of-organizations-say-they-are-not.html) of 600 senior security leaders, 73% said they would not be fully ready for a major attack tomorrow, and 89% cited limited executive or board involvement. Moving risk is a business decision, not just a security team task.

### Push harder on DevOps

Eric Raymond wrote "release early, release often" in *The Cathedral and the Bazaar* in 1997, and DevOps spent the next two decades turning it into practice: small batches, continuous integration, automated deployment, fast rollback. Security just made it mandatory.

Most teams can't patch quickly because shipping any change is slow. If you're two major versions behind on a framework, a security fix becomes an upgrade project. If every deploy needs a change board and a weekend window, the patch waits.

{{< callout >}}
If shipping a one-line fix to production takes a week, your patch SLA is a week, whatever the policy says.
{{< /callout >}}

So patch what's available now, then fix what makes the next patch slow: stay on supported versions, remove abandoned dependencies, automate the deploy, and agree on who can approve an emergency change. As Jez Humble and David Farley put it in *Continuous Delivery*, "If it hurts, do it more often."

### Use agents to build the tests

Releasing often only works with automated tests that tell you, in minutes, whether a change broke something. In *Accelerate*, Nicole Forsgren, Jez Humble, and Gene Kim found test automation was one of the capabilities that predicted high delivery performance.

The code that's hardest to patch is usually the code with no tests, because nobody wants to touch it. Writing those tests is tedious work people put off for years, and coding agents are good at it. Give them context on how your system works, like `AGENTS.md` files, and review what they produce. Every test they add lowers the risk of the next fast patch.

### Use agents to find and triage flaws

Attackers are already pointing frontier models at your systems. Do it first, and fix what you find on your schedule instead of theirs.

Then let agents take the first pass on every finding: reproduce it, check whether the vulnerable code is reachable, and score their confidence. People focus on the low-confidence and high-impact findings and spot-check the rest. AI still makes mistakes. In a [Stanford study](https://arxiv.org/abs/2512.09882), the best AI agent outperformed most professional penetration testers, but 18% of its findings were false positives. Catching those and making the calls is the job for people, not reading every row of a spreadsheet. It's the same model Vapor Panda used.

### Manage the risk you inherit

Most of the code you run, you didn't write, and you can only patch as fast as upstream ships fixes. Upstream is struggling too. In Glasswing's [first month](https://www.anthropic.com/research/glasswing-initial-update), Anthropic disclosed 530 high- or critical-severity bugs to open source maintainers, and 75 were patched. Several maintainers said they were "severely capacity constrained," and some asked Anthropic to slow down.

Open source is [free like a puppy](/blog/open-source-free-puppies), and its upkeep falls on whoever shows up. So show up. If you find or fix a flaw in a project you depend on, send the patch upstream with tests. That helps a stretched maintainer far more than another bug report.

For everything else, ask. Commercial vendors should be able to tell you their security response time and release cadence, and that belongs in the contract. Open source projects show theirs in public: release frequency, number of maintainers, and whether they have a security policy. Drupal makes this easy, because contributed projects are either covered by the Drupal Security Team's advisory policy or they aren't.

Then build a risk framework for your dependencies. CISA's directive is a good starting point: it sets deadlines from internet exposure, known exploitation, whether exploitation can be automated, and how much control a flaw gives an attacker. Add one more factor: how fast upstream can ship a fix. An internet-facing dependency with one part-time maintainer is a different risk than an internal library backed by a vendor SLA. Know what you run, rank it, decide which dependencies need a backup plan, and revisit the list often.

## Deliver with confidence, faster

The bets placed on slow attackers no longer pay off. The new bet is on speed you can trust: shipping a safe change to production in hours, routinely, without heroics. That means less manual effort at every step, with agents writing tests and triaging findings, and people spending their time on the decisions that need them.

If a critical CVE dropped tonight in your most important dependency, how many hours would it take to get a tested fix into production?
