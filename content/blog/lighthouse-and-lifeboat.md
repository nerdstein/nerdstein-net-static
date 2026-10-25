---
title: "The Lighthouse and the Lifeboat"
date: 2026-10-25
slug: "lighthouse-and-lifeboat"
tags: ["leadership", "reflection", "engineering"]
description: "Proactive and reactive leadership are both strengths. The skill is knowing which one the moment, and the company, needs."
draft: false
---

In 2001, Nelson Repenning and John Sterman published a paper in the *California Management Review* with one of the best titles in management writing: "Nobody Ever Gets Credit for Fixing Problems that Never Happened."

That title names something it took me close to 25 years of experience to learn. The places I've worked rewarded different ways of working. Some ran on urgency, where the job was to spot the most important problem and chase it down. Others ran on planning, where a quiet week meant things were working.

For a long time I assumed one of those was the right way and the other was a phase to grow out of. It took seeing both, more than once, to understand that neither is the right way. They're two different strengths, and the setting decides which one you need.

![A lighthouse on a calm cliff casts its beam over quiet water, while further out under a storm cloud a lone rower pulls a small boat through heavy waves.](/images/lighthouse-and-lifeboat.svg)

## Two jobs on the same coast

A lighthouse keeper and a lifeboat crew both keep sailors alive. The keeper makes sure ships see the rocks. The job is routine, and when it goes well nothing happens. The lifeboat crew goes out into the storm after something has already gone wrong, and everyone sees it.

Every coast has boats that need both: a lighthouse to guide them past the rocks, and a crew for when one hits them anyway. Both do their part to keep the boats afloat.

In *The Last Word on Power*, Tracy Goss calls the patterns that got you where you are your "winning strategy," and warns that it becomes a trap once you stop choosing it and run it by default. Proactive and reactive are the two winning strategies I see most in leadership. Most teams can tell you which one their leader defaults to within a week.

## Why the quiet gets no credit

Repenning and Sterman describe what they call a capability trap. A team under pressure skips the improvement work to deal with today's problems, which creates more problems, which leaves even less time for improvement. Firefighters are visible and get rewarded, so the organization learns to value firefighting. A proactive leader sets out to make the week calm and boring, and gets little credit when it works.

Eisenhower named the tension in a 1954 speech at Northwestern University:

> I have two kinds of problems, the urgent and the important. The urgent are not important, and the important are never urgent.

Stephen Covey later built his time-management quadrants on that idea. Reactive leaders excel at the urgent. Proactive leaders invest in the important.

## What the extremes cost

A fully reactive leader burns people out. In 2019 the World Health Organization recognized burnout as an occupational phenomenon resulting from "chronic workplace stress that has not been successfully managed." A crisis now and then is part of the job. A crisis every day is a choice about how the work gets run. Fires also suck the air out of the room, so the roadmap, the cleanup, and the hard conversations all wait. And a team led by a firefighter learns to wait for the next fire.

A fully proactive leader has a different problem. If nothing ever goes wrong, it's fair to ask whether anyone is trying anything that could. Taking risks is how a team grows and how a business stays competitive, and some of those risks will start fires.

## Where are you spending your time?

Time is the one thing every leader invests, and where you put it should match where the effort is. My own career taught me this part most clearly. Every effort is a pursuit of stability, because people crave routine and predictability. Uncertainty wears on us more than we expect. In a 2016 study published in *Nature Communications*, researchers at University College London had people play a game where turning over rocks could reveal a snake and a mild electric shock. Their stress tracked how uncertain the outcome was, and it peaked when a shock was a coin flip, not when it was most likely.

A new product or a young company lives in that uncertainty. Most days really are surprises, and time spent reacting is how you learn what works and find stable ground. As the effort grows, the return on that time shifts. Prevention, structure, and process start paying off more than chasing the next fire.

Larry Greiner described this in "Evolution and Revolution as Organizations Grow," published in *Harvard Business Review* in 1972. In his model, companies grow in steady stretches, each ending in a crisis that forces a change in how the company is run.

![A hand-drawn growth chart: an organization climbs through calm stretches of steady growth, each one ending in a short, jagged crisis before the next stretch begins.](/images/greiner-growth-phases.svg)

The first, growth through creativity, ends in what Greiner called a "crisis of leadership," when the founders' informal, hands-on style can't run a larger organization anymore. To get past it, the company has to turn its fires into structure and process.

His crises go both ways. Growth through coordination ends in a "crisis of red tape," when the systems built to bring order start getting in the way of the work. That's the proactive extreme. The fix for each stage eventually causes the next crisis, which is Goss's winning strategy at the scale of a whole company.

## The tension between dev and ops

My most direct technical lesson in this came from DevOps. Development is the proactive side: planning, code review, tests, and gates that catch problems before they ship. Operations is the reactive side: pagers, incidents, and on-call for whatever gets through.

Kept apart, the two pull against each other. Developers are rewarded for shipping change, and operations is rewarded for stability, so every release turns into a negotiation. DevOps grew out of that friction. Werner Vogels summed up Amazon's answer in a 2006 interview with *ACM Queue*: "You build it, you run it." When the same team owns both, it has to keep balancing proactive and reactive work, and it's directly accountable for its own problems. There's nobody else to hand the fire to, so incidents feed straight into better tests and gates.

Google's Site Reliability Engineering practice puts a limit on each side. SREs cap operational work at 50% of their time, and error budgets treat a service that's too reliable as a sign the team isn't shipping enough.

## What I watch for now

The biggest leadership lesson in all of this, for me, is that I can't pick one mode and stay there. I have a default, like everyone does, and I drift toward it. What I've had to build is the other mode, and the awareness to notice when my team has tipped too far one way.

The signs are usually easy to spot once I look. If every conversation is about the latest incident, the roadmap hasn't moved in weeks, and the same people get pulled into every fire, we're too reactive. If the plans are thorough, nothing has gone wrong in months, and nobody can name a bet we've made that might fail, we're too proactive.

Fires teach us what to prevent, and calm gives us room to take risks. Every coast needs a lighthouse and a lifeboat crew. My job is to notice which one we're short on.
