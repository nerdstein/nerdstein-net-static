---
title: "A DevOps Primer"
date: 2019-04-29
slug: "devops-primer"
tags: ["development", "people"]
description: "DevOps is a philosophy, not a product — a primer on the foundational concepts and why they align naturally with agile ways of working."
draft: false
---

I just closed about 100 browser tabs from an early year activity. While it’s embarrassing I left those tabs open so long (going on five months), I wanted to leave them open to reflect on what I learned. And, what a better way to reflect than a blog post.

# The Soapbox

Bear with me for a moment. I subscribe to the philosophy that DevOps represents a line of thinking and a way of working, not a technical product. Like security, when someone says, “I’ll sell you DevOps”, it’s a scam. For those “doing” it right, you need to focus on foundational concepts built into continuous learning. This ideology has been communicated in talks and blog posts by some of our communities’ sharpest minds, including [Michelle Krejci](https://twitter.com/dev_meshev), [Jeff Geerling](https://twitter.com/geerlingguy), [Mark Schwartz](https://twitter.com/schwartz_cio), and more. And, in my opinion, there is a direct correlation to Agile frameworks. Concepts like retrospectives to share learnings, sprint planning to prioritize, and backlogs to organize and track work thoughtfully. Most of these ceremonies are open to the whole team to participate, so they naturally advocate for transparency and connection.

Key point: DevOps is ongoing evolution through experience. Technical progress is just one type of outcome, but equally important are solutions involving people and process.

# DevOps Philosophy

Change is at the heart of DevOps. Digital products change. People change. Organizations change. DevOps reflects a pragmatic approach to change. Many people discuss it, especially solutions. But, any solution reflects a change that is, hopefully, driven by what is learned and what can deliver better, more impactful results for actual people and real problems encountered.

As a basis, start by evaluating what change occurs. On the surface, change can look like any of the following:

- System and software updates, especially security ones

- Continuous Integration (deployments of change increments, automated/manual processes)

- Changes in the team (people leaving, people being promoted to new roles)

- Organizational changes (launching a new product, leadership transitions, exploring new markets)

- Incidents (getting hacked, services going down)

- Exploring new technology

- Sunsetting legacy technology

A mature DevOps practice is capable of adapting to change ongoing and remaining effective. An equally important philosophy is the openness and willingness to change. This is built on trust and the recognition that every team member is capable of bringing value: to allow people to raise their voices, drive change, and have impact.

DevOps can be transformational. It can be really hard and a non-natural fit for the “command and control” models traditionally established with embedded IT departments and IT vendors. Mark Schwartz writes about this concept routinely in [blog posts](https://aws.amazon.com/blogs/enterprise-strategy/shu-ha-ri-detaching-from-and-transcending-command-and-control/) and in his book “A Seat at the Table: IT Leadership in the Age of Agility.” Again, organizations suggesting they can just buy DevOps would be in for a rude awakening or really only purchase an incremental step relevant at that point in time only. Sure, you can purchase a two million dollar Kubernetes, cloud-based infrastructure framed as DevOps. But, what problem are you really trying to solve? Chances are, you’ll be in a position of opening up countless other problems around vendor lock-in, governance, maintenance, and enablement you never anticipated. A better place to start is in the cultural change needed to identify problems, define risk, share ideas and make smarter investments capable of having real impact now and in the future.

# Bare Minimum DevOps

Now that I’ve set the context for my thoughts on what DevOps actually is, how do you do it? I’ve long wanted to make a blog post defining some bare minimum DevOps concepts. I’ve seen so many differences when I interact with a client or project. I’ve wanted to point back to something and highlight my thoughts foundationally. The range of differences reflect the varying states of learning organizations are at. And, it’s natural given many of the concepts represent years of learning how to build quality, robust digital solutions that are capable of adapting to change.

# Case Study: SimplyTest.me

Remember the browser tabs and the learning I did? I was working on SimplyTest.me. As of right now, it is a perfect example of a system desperately needing some DevOps love. There has been a lot learning and needs are defined. As the project lead, I’ve long wanted to automate routine failures, establish a more easy-to-change system, and open up SimplyTest.me for broader contribution. But, the current system is very hard to do so as it’s developed. The infrastructure is highly customized, the tool is fairly complex, and, subsequently this makes it harder to change. This may make for a future blog post, but the concepts shared reflect this recent exploration for SimplyTest.me and things I’ve encountered over the years.

# Environments

Change cannot and should not happen only on production systems. Any change needs prepared, tested, and then deployed to prod. At a minimum, you need both production and non-production environments. Change increments then get vetted through non-production environments before being released to production. A non-production deployment helps vet any changes made on a local system before they hit production.

# Parity

Parity is a key concept for evaluating change. As an example, if you are running different versions of PHP across environments, evaluating a change increment on one environment may not match the results of what gets deployed to production.

# Evaluation Criteria

If you change things, you need to establish a means for evaluating the change. This could be both manual or automated testing of a change. It could also be part of your development workflow on what needs to be tested when implementing a change. But, the key is you need to have some process defined. And, this process needs to respect both the change increment itself and some means of looking at regressions throughout a system. Because, any change made in one part of the system can unknowingly impact the rest of the system. Establishing some criterion to evaluate change may be just as important as the change itself.

This is not confined to technical change either. When making process or organizational change, there should be some metrics and data used to measure efficacy. After all, if you are making a change, how do you really know if the change worked?

# Source of Truth

Also known as the “system of record”, a source of truth is a data integrity concept. Some aspects of environments are more flexible to change than others. Most production systems maintain data (users, content, files, etc) that most likely should not change as change increments are deployed. And, non-production systems leverage production systems as the source of truth, often by synchronizing or replicating a “point in time” snapshot of the data to mirror production data before a change is evaluated. The source of truth is left untouched until the change is ready and often throughout a deployment of a change. Third party systems may be the source of truth for other enterprise functions. For example, an email server may be the source of truth for notifications sent from a system. Recognizing the differences and responsibilities of specific systems and environments help understand source(s) of truth and how they serve a larger change process.

# Backups

Even with the best of intentions, changes can break things. Be prepared at any point to restore from a backup, both by rolling back changes and by restoring databases. Test this process (really… it needs to work in the most inopportune of times). Having timely and relevant backups are hugely important for restoring botched deployments, standing up systems after a security incident, and generally gives people piece of mind. Make sure you understand how to restore a backup and bonus points if both the backup and restoration processes are automated.

# Keys

Identity management is a really deep and hard problem in IT. On the surface, people think identities apply only to users. But, systems need a proper way to be identified and subsequently verify their authenticity. Keys are a widely adopted approach. Often there is a public and private key, where the public key is referenced by other interacting systems. The private key is used as the verification and is owned strictly by the system. Maintaining keys is a critical way to ensure only specific systems are capable of accessing and associating a system to another (often through users and their specific permissions).

# Secured Channels

When systems are interacting, one needs to be concerned with the channels in which systems communicate. Secured channels help encrypt communication. The most common of which is the use of SSL and certificates. Tools like LetsEncrypt have brought SSL to the masses, allowing for a free way to generate (and re-generate) SSL certificates capable of happening in an automated fashion. This helps mitigate the risk of someone intercepting and browsing your traffic between systems.

# Scripting

One key way people apply what they have learned is through scripting things that happen routinely. Scripting also can be as simple as a Bash script to perform a routine operation in a consistent fashion or a robust development framework with conditional scripts executing routinely and on-demand. Those intimidated by scripting can start off basically by leveraging tried and true bash scripts that run non-interactive commands across any environment. You can get a long way without introducing complexities found in more robust frameworks.

# Code Repositories

Code repositories are the cornerstone of DevOps. They are the source of truth for all system code, any scripts that run, and can be critical in any disaster recovery/restoration process. Code repositories maintain a record of changes and the users who made the change. Code repositories can be cloned to any environment and fetched as needed (the “D” in “DCVS”). Concepts like branches allow for changes to be staged before being merged into a branch associated with production environments. Releases can be implemented as tags that reference specific commits. And, many popular tools (Github, Gitlab) offer features, like pull/merge requests, that are advantageous within a development workflow.

Also, code repositories maintain change events. Creating a new branch may provision a new environment (this has been made popular by CI/CD models) that allow for hands-on testing of changes before release. Merging a branch can destroy an environment and trigger a deployment to a production or non-production environment. And, tools like pull/merge requests allow for code to be reviewed. All of these events are exposed to a broader opportunity that DevOps can leverage. For example, running automated tests can occur when commits are pushed up to a branch or when a deployment to a non-production environment occurs. None of this is possible without a code repository.

# SSH

When events occur and scripts need to be run, how do they run on the actual systems? SSH is the answer. SSH is the protocol used to remotely execute commands from one machine to another. I remember the days where every company had huge in-house server closets with expensive terminals to manage the servers. Now, we can purchase affordable infrastructure managed remotely, upload keys, and open terminal sessions that are directly connected to these remote machines. SSH has made much of this possible and is critical for DevOps.

# Jenkins

Continuous integration (CI) tools exist to centralize and execute what you have automated. I questioned if this needed to be on the “bare minimum” list. Inevitably, you can do a lot without such a tool, but you won’t get the mileage you could otherwise. CI tools do a great job of logging execution and maintaining a history of execution. Imagine developers having to save their terminal history. Such tools help teams have a central platform where multiple users can log in, access can be control, parameters can be selected to use common scripts, and more. Tools like Jenkins, Travis CI, and CircleCI have native integration with code repositories, can help manage keys and servers, and can manage complex, conditional workflows.

# Systems Infrastructure

All of the aforementioned concepts rely on an infrastructure that runs the systems. At a minimum you need at least one server for production and seperate server(s) for non-production infrastructure/environments. Backups should be maintained offline and outside of the servers.

# Infrastructure as Code

While it’s not “bare minimum,” container-based, cloud technology can create a flexible infrastructure capable of provisioning and tearing down servers when change events occur. This maintains a durable, extensible infrastructure capable of responding to change. Tools like Docker can help create the definition and images needed for containers. Cloud-based platforms have APIs for creating instances as needed, managed volumes for persistent storage (logs, databases, objects/files), and monitoring needed for auto-scaling. Production infrastructure, or specific aspects of it, should be persistent. Load balancers and proxying become common when implementing this type of infrastructure, including DNS management. Again, while this may not be completely necessary, it’s certainly an appealing option for those building something from the ground up or people looking to level up an existing infrastructure.

# Documentation

This may seem commonsensical, but there must be documentation. At a minimum, I look for a README in the code repository, describing how to set up a project, a technical architecture overview, a description of the infrastructure, and a brief rundown of what is found in the code repository. Non-technical users often need Google Docs or something outside of the technical repository. The most common things I’ve seen are flow charts articulating the DevOps workflows, diagrams of the systems, and high-level commentary on insight and motivations. After all, changes in teams or members on teams can be caught completely flat footed without good documentation.

# Summary

As I shared, I think DevOps is sometimes a misrepresented topic because I believe it starts with a way of thinking, is often associated with transformation, and is not strictly about technical outcomes. I’ve seen variations in maturity and tried to share what I consider to be a bare minimum set of concepts people need to both practice and apply DevOps. I can’t imagine the number of browser tabs I’ve opened over the years researching this topic. Again, it’s simply not enough to purchase a product and expect the potential outcomes. What do you consider DevOps to be? What set of bare minimum concepts did I miss?