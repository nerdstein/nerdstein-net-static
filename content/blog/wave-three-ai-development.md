---
title: "Wave Three: A Framework for Rolling Out AI on Engineering Teams"
date: 2026-07-01
slug: "wave-three-ai-development"
tags: ["ai", "engineering", "leadership"]
description: "AI adoption in software teams has moved through three distinct waves. Wave 3 is where the real work begins: centralized knowledge, autonomous operations, and governance by design."
draft: false
---

The subsidized experimentation period is ending. AI vendors built market share through discounted pricing, free tiers, and trial credits. That phase served its purpose. Now, with usage established, pricing is moving — and teams are being pushed to treat AI as a managed investment rather than a free experiment.

Price pressure is useful. It forces the question most teams have avoided: *what are we actually getting from this, and are we doing it right?*

These are my views on how to think about that question — and what a mature, well-run AI rollout looks like for an engineering team.

---

## The Three Waves

AI adoption in software teams has followed three recognizable phases. Most teams know where they've been. The question is where they're going.

- **Wave 1 — Exploration**: Individual experimentation with no shared strategy. GitHub Copilot subscriptions, Codex integrations, early Claude Code trials, Cursor experiments, local model setups. Appropriate for its time — you can't develop judgment about tools you haven't used.

- **Wave 2 — Adoption**: AI gets rolled out to teams — licenses purchased, tools provisioned, usage encouraged. But without governance or shared practice, adoption is unstructured. *Personal*: each developer builds their own habits, workflows, and prompting approaches in isolation. *Local*: each person selects their own harness, models, and integrations independently. Institutional knowledge stays in individual heads and doesn't transfer.

- **Wave 3 — Maturity**: Intentional, governed, scaled AI practice. Shared knowledge repositories. Autonomous operations integrated across the SDLC. Cost management tied to outcomes. Human-in-the-loop gates defined by design, not discovered after something goes wrong.

These waves follow the same arc as any core technology moving through its lifecycle. The standard technology lifecycle defines four phases:

- **Innovation / Incubation**: Research, development, and early prototyping. Costs are high, returns are negative. Experimentation is the right posture.
- **Growth**: The technology reaches wider adoption. Initial investments are recouped and teams begin scaling usage.
- **Maturity**: Widespread acceptance takes hold, but growth slows. The focus shifts from exploration to optimization, governance, and sustained value extraction.
- **Decline**: Superior alternatives emerge and the current approach eventually becomes obsolete.

AI in software development has moved through Innovation/Incubation (Wave 1) and Growth (Wave 2) and is entering Maturity (Wave 3). The patterns that define mature technology adoption — standardization, cost discipline, governance, institutional knowledge — are exactly what Wave 3 requires. The rest of this post describes what that looks like in practice.

---

## Why Wave 2 Isn't Enough

Staying in Wave 2 creates compounding risk as AI use deepens:

- Every developer rebuilds the same work: their own agent definitions, skill definitions, harness configurations, and system integrations — none of it shared.
- No common understanding of which work is well-suited for AI and which isn't.
- Token spending is ad hoc, with no visibility into what's producing value.
- AI is non-deterministic. It produces plausible output, not correct output. Without shared validation patterns, errors scale with usage — and the opportunity cost compounds equally. The inverse is also true: shared learning and contribution to common capabilities is what enables continuous improvement. Each team member's discovery improves the shared foundation for everyone, naturally building the kind of compounding institutional knowledge that defines mature technology practice.
- When something goes wrong — a hallucination committed, a security vulnerability shipped — there's no audit trail and no defined process for catching it.

The dynamic Christensen described in *The Innovator's Dilemma* applies here: organizations don't fail because they ignore new tools. They fail because they adopt them in ways that preserve existing patterns rather than rethinking the underlying process.

---

## Wave 3 Patterns

### 1. Centralized Knowledge

**Definition**: A shared repository of agent definitions, skills, contextual instructions, and prompt libraries that the whole team contributes to and benefits from — reviewed and maintained like any other shared codebase.

In practice:
- Shared `CLAUDE.md` files and skill definitions checked into source control — these are the core definitions that govern AI behavior across the entire SDLC. They are not peripheral configuration; they define how agents understand your codebase, standards, and team practices, and integrate directly into every downstream system: CI/CD pipelines, code review workflows, autonomous agent operations, and product integrations. When these definitions are shared and version-controlled, every SDLC touchpoint benefits from the same institutional knowledge
- MCP servers any team member can connect to for common context
- LLM gateways that centralize logging and usage visibility
- CI/CD-integrated agents with defined triggers and outputs
- Contribution model mirrors software engineering: pull requests with human and AI-assisted review before merge

The underlying principle is the same one that makes open communities outperform siloed ones: knowledge shared openly compounds. Individual discoveries become collective capability. The AI practice improves with every contribution rather than resetting each time someone joins or changes tools.

This scales from a single product team to enterprise platform engineering. The pattern is the same at any size.

### 2. Spec-Driven Development

**Definition**: Explicit, structured specifications that define the expected behavior, output, and success criteria before AI work begins — aligning execution with business requirements upfront rather than discovering intent through iteration.

In Wave 2, AI was used reactively: a developer encountered a problem and reached for a tool. In Wave 3, the work is defined before AI is invoked. Specifications narrow the problem space, reduce hallucination risk, and create a shared contract between business intent and technical execution.

In practice:
- Proper upfront definition and context: requirements and acceptance criteria developed with enough clarity that AI can act on them without filling in gaps through assumption. This means leveraging AI feedback loops to question and pressure-test the specification itself before any execution begins — surfacing ambiguity and misalignment when they are cheapest to resolve. The goal is to shift left: catch the wrong problem, the unclear requirement, and the missing constraint before a single line of code is generated
- Specifications bridge business goals and technical implementation: what needs to be built, for whom, and what "done" looks like — defined before a line of code is generated
- Specs treated as first-class planning artifacts — maintained in team backlogs and roadmaps alongside other work, not buried in chat threads or throwaway documents
- Output validation against specs as part of every review: not just "does it work?" but "does it meet what was defined?"
- Business stakeholders engage at the spec level, not the code review level — shifting alignment earlier in the process where it is far cheaper to correct

### 3. Autonomous AI Operations

**Definition**: AI that automatically responds to events across the SDLC — without a developer needing to watch for, trigger, or invoke it locally. When a pull request opens, an agent reviews it. When a build fails, an agent diagnoses it. When a ticket is created, an agent acts on it. The AI operates on the same event-driven model as any other automated system in your pipeline.

This is the sharpest break from Waves 1 and 2, where AI was entirely local and developer-initiated. Autonomous operations move AI from a tool individuals pull into their workflow to a system that responds to the work as it happens — at scale, continuously, with only defined human-in-the-loop gates.

In practice:
- Agents triggered by pipeline events: pull request opened, build failed, ticket created, deployment completed
- Automated code review, test coverage generation, and security flagging — running on every relevant event, not on request
- Jira and project management integration: tickets created, assigned, and updated by agents based on defined triggers
- Project management tools and backlogs serve as the system of record for agentic actions — logging what agents did, what they deferred, and what was escalated for human review. Agentic work should be as traceable and maintainable in Jira as human work, making autonomous operations visible across the team without anyone needing to watch agents directly
- Defined output modes per event type: read-only guidance for lower-risk operations, write operations for well-defined and validated workflows
- Clear escalation paths: autonomous action within defined bounds, with human-in-the-loop gates for decisions outside those bounds

### 4. Systematic Governance

**Definition**: Human-in-the-loop gates, cost discipline, and contribution controls defined upfront — the framework that makes autonomous operations safe, sustainable, and aligned with business priorities.

In practice:
- Human review gates established before deployment, not improvised after incidents
- Read-only guidance modes before write operations, based on risk level
- Audit logging so you can reconstruct what happened when something goes sideways
- Consistent contribution reviews for shared agent and skill repositories

**Cost governance** is not about token budgets and metering — that is an IT mindset that introduces artificial friction and punishes productive use. The right frame is: does AI spend map to business outcomes and priorities? AI that is producing real value will consume tokens, and capping spend arbitrarily is the wrong control. The effective levers are:
- **Model selection as a governed decision**: most day-to-day tasks do not require a frontier model. Wire the right model into shared agent definitions and harness configurations by default — complex reasoning and high-judgment work gets frontier models; routine, high-volume, and well-defined tasks use smaller, faster, cheaper options
- **Cost measured against outcomes**: track what AI spend produces — velocity, defect rates, time saved — and reallocate toward the work where the return is highest
- **Prioritization over caps**: direct AI effort toward the highest-value work rather than imposing blanket limits that treat all usage as equal

Governance applies to both the shared knowledge repository and the autonomous operations it powers. This is the same discipline responsible teams apply to any system with production consequences.

---

## What This Means for Developers

The industry has treated software as a fixed asset — something built, owned, maintained, and periodically revamped. If code can be generated on demand and rebuilt from a spec in hours, that assumption is fragile. The conversation shifts away from *which language, which framework, which architecture* toward *what produces the right outcome with the fewest tokens, the fastest time to market, and the lowest cost to change*.

Fred Brooks argued in *The Mythical Man-Month* that the hard part of software isn't the code — it's understanding what the system should actually do. That argument becomes more true as code generation gets cheaper.

What this means for developers on Wave 3 teams:

- **Review is still the job** — it just happens faster and at higher volume. Reviewing AI-generated code for correctness, security, and architectural coherence is still review.
- **Judgment is the differentiator** — catching problems early, evaluating whether a solution solves the right problem, understanding enough business context to know when the output is right.
- **Using AI to produce output without being able to evaluate it is a liability**, not an advantage. Plausible-looking mistakes ship just as fast as correct code.

{{< callout >}}
The developers who succeed in Wave 3 use AI to amplify judgment, not substitute for it. Planning carefully, verifying outputs, and staying accountable for what ships — those are not optional extras. They're the job.
{{< /callout >}}

---

## The Work of Wave 3

Every technology that has mattered goes through the same arc. Cloud computing, DevOps, agile — all followed the Innovation/Incubation → Growth → Maturity pattern. The organizations that navigated maturity well built durable, compounding capability. Those that treated widespread adoption as the finish line found themselves managing inconsistency rather than extracting sustained value.

AI is at that inflection point now.

The three patterns in this framework are already the practices that distinguish teams with genuine AI maturity from those still in Wave 2: centralized knowledge that compounds with every contribution; autonomous operations that respond to events across the SDLC without waiting to be invoked; governance that makes those operations safe and cost-effective without the friction of arbitrary controls.

Getting this right is an organizational challenge, not a technical one. The models exist. The tools exist. What most teams lack is structure — shared definitions that govern AI behavior consistently, event-driven operations that scale beyond individual effort, and oversight proportional to risk rather than reflexively restrictive.

The developer's role doesn't disappear in this model — it clarifies. The judgment to know what to build, the expertise to evaluate whether the output is right, the discipline to hold the line on quality when AI makes it easier to skip that step. Those capabilities don't get automated. They get amplified — or they get exposed.
