---
title: "Engineering Tenets of Agile"
date: 2015-10-21
slug: "engineering-tenets-agile"
tags: ["development", "people"]
description: "Five engineering practices — from CI/CD to simplicity to user focus — that complement agile rather than conflict with it."
draft: false
---

## Background

I recently changed companies and am going through the process of onboarding. One of the big draws to the new company was an emphasis on people and culture. The whole balance between a for-profit business and a focus on employee needs, in my experience, can be in conflict. I have been learning more about how these goals are achieved.

In some onboarding documentation, there has been a reference to "The Agile Manifesto". A swift Google search, let me to [this page](http://www.agilemanifesto.org/).  The core values are defined as follows:

> Individuals and interactions over processes and toolsWorking software over comprehensive documentationCustomer collaboration over contract negotiationResponding to change over following a plan

On the surface, these serve as guideposts for process. This complements quick, yet adaptive models to support ongoing change management. I believe the same principles apply to engineering practices as well.

## DevOps and Continuous Integration

Continuous integration is all the rage. It also happens to perfectly support Agile practices. Continuous integration practices advocate for an ongoing evaluation of development practices. The key is "ongoing", as it's an acknowledgement that operations should evolve over time. Engineers should be free to bring up feedback on processes, prioritize that feedback, and research ways to solve issues raised. Engineers can be creative and innovate in ways to positively impact the team. Many tools support these practices, like Github, TravisCI, Jenkins, etc. Tools are great but need to be evaluated for platform-level integration, bigger picture perspectives, and strategic impact.  

## Focus on quality

Agile practices may see frequent and ongoing changes that impact scope, the project team, and the deliverables. This highlights a need for consistent and polished engineering practices. Too many degrees of freedom will yield too much variation at critical times a project may need to scale resources or hit a key deadline. Plus, the quality of engineering deliverables will suffer without consistent checks and balances.  Scope and priorities may change, but the engineering practices should advocate for predictability. Consider ticket-level code reviews/qa checks after development completes, ticket-level technical discovery before development begins to get ahead of any lack of requirements, and a clearly defined support process when issues arise. 

## Release early and often

I believe long release cycles violate Agile practices. Change cannot be quick if releases are not. Engineering practices should strive to get deliverables into the hands of the stakeholders as soon as possible to get the feedback needed. This also helps pair back the scope of issues that arise during deployments, easing release management. Practices should include ongoing releases and/or short release cycles (in lieu of fixed releases), advocating for rapid prototyping, clearly defining expectations around level of completion (what does "done" mean to you?), and feedback loops. In short - practices should be very iterative. Code organization should be discretely organized and the use of code repositories can assist with change management (see history, revert to a previous iteration, etc).

## Simplicity over complexity

Simplicity is complementary to change. The most simple solutions are often the most elegant. Complex solutions add technical debt and are often velocity killers. Often, complex solutions are difficult to iterate on, they cannot be done quickly to iterate and/or prototype, and they produce institutional knowledge that create challenges for handoff. Projects can rarely avoid complexity (if everything was easy, we wouldn't be paid to do it), but it should be actively mitigated during code review and/or an evaluation of the best solution per-ticket. This strives for engineers to follow and observe best practices (e.g. properly leveraging a development framework, code-level comments, technical architecture documentation) to ensure a potential handoff is clean (other team members, the client, etc).

## User-driven development

Engineers need to maintain a focus on who the product serves. This could be visitors to a site, marketers entering content, or developers and maintenance. An avoidance of this perspective, in the face of change, creates chaos. Engineers should be proactive about spot checking their work, being thorough, and mindful of regressions. A ticket may state explicit steps for QA, but developers should be mindful that their work may inadvertently create an issue. An engineer self-check and brief analysis of any random observations can avoid introducing bugs that a client may see (and subsequently report later). This can be compared with any existing development (check another environment if something has been introduced) and, if possible, address it within the development of the ticket. If it is larger, consider adding another ticket and updating the QA steps of the existing ticket.

## Summary

As engineers, we need to understand how best to complement Agile practices. Thankfully, there are clear and well understood paradigms that help with this. And, of course, iterate, learn, and evolve.