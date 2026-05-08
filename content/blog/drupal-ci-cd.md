---
title: "Drupal CI/CD with TugboatQA and Github Actions"
date: 2020-12-29
slug: "drupal-ci-cd"
tags: ["development", "drupal"]
description: "Vacation this year has been amazing."
draft: false
---

Vacation this year has been amazing. I've caught up on some of my long-standing to do list, like launching this new nerdstein site and digging into some of the newer technology I've wanted to explore. SimplyTest has some great new contribution I am excited about. I've spent a ton of time with the kids coloring, playing, and just enjoying these moments while they are young. It is shocking how quickly they have grown. I've cooked a lot and those close know how much I enjoy doing that. I've blogged more - finally - after a long hiatus and lack of motivation. I am currently enjoying an Eight & Sand Brewing - *Loco Mo Sim DDH* and listening to the Gravity album from Our Lady Peace. The kids are currently asleep. I wanted to share some things I've explored today.

Automation is important for consistency and for ease of use. It's one of the tenets of DevOps. Automation is the cornerstone of creating a great experience with SimplyTest.me. I've spent years creating continuous integration solutions for customers to help them be more effective. Yet, I never did that for my personal website... until now.

Building off of my new website launch, I wanted to keep the momentum going. Recall from my blog post yesterday, I set up the basics of TugboatQA to replace my development server with something more modern. I also set up a new Linode for my production server. I wanted to learn Github Actions for deployment automation, as I had never used it. I desired to have an end-to-end CI/CD pipeline built completely with GitOps. And, I wanted as much of this automated as possible.

I was pleasantly surprised with how smoothly things went. Maybe I shouldn't be, as I'm basically building a pipeline for a simple website. Let me share a bit more about this experience should you find it beneficial.

## Pipeline

This pipeline basically happens in the following workflow:

- I work locally and push changes to a branch to Github (Composer, custom code, config, etc)

- I make a pull request for this change off of the branch

- Pull requests are subsequently deployed into their own Tugboat environment (executes a fresh environment that pulls production databases and files with automated deployment)

- I review the code for anomalies or missing things like config

- Manual testing occurs on the Tugboat environment (note: I need to work on automated testing; I plan to implement the visual regression test of TugboatQA in the future)

- The pull request is merged after it passes my thorough review ;)

- A production deployment happens once the code is merged

For the sake of what I consider novel, I'm going to focus on two main areas of this pipeline: **TugboatQA** and **Github Actions**. I assume a production server exists, but I will describe what is needed to manage assets from production (the source of truth for content in Drupal). And, I assume people are good with the well-documented pull request workflow methods. Please reach out if any further details would be helpful.

## Commentary: Drupal Assets

My production site is a basic LAMP stack with some specifics for Drupal, like Composer and Drush (site local, of course). Any true Drupal development workflow needs to readily be able to get databases and files from production as the source of truth. Files are relatively easy with the Stage File Proxy module in Drupal, which can replace local files with those served remotely. Drush Aliases are a great way to do the database backups. But, I wanted to avoid putting credentialed data that into a public repository (note: these features are often offered by Drupal PaaS providers and you should use it). I opted to generate a script that could be invoked upon deploy and used *mysqldump* to create a gzip'd SQL file on-demand. Easy peasy bash script-ezy (sorry, I'm watching too much Food Network during this pandemic hell).

## TugboatQA

TugboatQA replaced my development environments with automated environments per change (pull request). TugboatQA natively has Github integration and the Tugboat repository settings allow for new environments to be provisioned upon pull request.

Tugboat's infrastructure-as-code capabilities resemble Docker Compose (I denote this as the services layer), but Tugboat has specific hooks that allow for automation scripts to run at specific events within the lifecycle of an environment. The offering is catered for building great environments in a variety of platforms. As such, the services layer is readily configurable, allowing it to have parity with the Linode server tied to a set of Docker-based images. I'll probably try this out for a NodeJS-based workflow in the future. 

I was able to add in the basic Drupal deployment steps into these hooks for the desired automation. This can and should be specific for your project. Mine did the basics: Composer install, drush config import, drush update database, and drush cache clear.

Finally, TugboatQA generates a public and private key for every project. I was able to create a locked-down, Tugboat-specific user on my production server where I copied the TugboatQA public key into the *authorized_keys* for that user. This allowed me to explicitly control  what Tugboat could and could not do within the server. This allowed me to only have Tugboat run a script on production that made a database backup and leveraged *scp* to retrieve the generated backup into the Tugboat environment. 

### Example

You can see how I've configured the TugboatQA behavior through its config.yml directive:

## Github Actions

I wanted something to kick off a production deployment. Much like AWS Lambda, this type of capability only needs to execute a script which is in sharp contrast to a more persistent, permanent server like production. This deployment automation only needed to happen after I reviewed a change in Tugboat and after I merged a pull request. Github Actions had just what was needed to do this.

### Secrets Capability

One of the "secret" sauces of Github Actions is the integration of their secrets feature. Think of this as a private, secure key value store. Instead of committing scripts with a bunch of private information (keys, server IPs, usernames, passwords, etc), you can store your secrets in the repository settings and pull them within committed, ever changing scripts. Very cool.

### Events

I only need my production deployment to happen after a pull request is merged into *master*. This signifies that a change has been reviewed, tested on Tugboat, and it is not expected to break a bunch of stuff.  Github does not explicitly have a pull request creation or merge event in Github Actions. However, on further thought, what I really care about is when I push code to *master*. Suppose I have a hotfix, like a security update in Drupal. Yes, I *should* push this through normal channels. But, time is of the essence. So, I may want the opportunity to commit code directly to master. Yes, this *can* break things but I can't rule out the possibility of needing to do this if I feel like it needs to be done (process for the sake of process is not effective). Pushing *any* code to master actually covers me for any deployment I care about - a hotfix or a pull request. I focused on this *code push* event for the basis of a production deployment, which was supported by Github Actions.

### Automation

Much like Jenkins is commonly leveraged as a CI tool to automate remote deployments, I didn't want Github Actions to do much more than serve as a proxy to my production server. In a similar fashion to Tugboat, a Docker image can be leveraged in each step of a Github Action "used" to execute steps of your workflow within a specific runtime. I chose a simple "SSH Action" image that allowed me to run commands remotely with a clean abstraction to SSH into my production server. I was able to readily embed my secrets into this script thanks to this abstraction, which had parameters for the SSH credentials that I embedded the secrets into. 

Like what I did with Tugboat, I added deployment commands for the basics of a Drupal deployment. I updated Composer and leveraged Drush to update the database schema, import the config, and clear the cache. One notable difference was pulling in the most up-to-date code from the *master* branch. If I had something more complex, this could have accounted for environment-specific differences with tools like *Config Split*.

### Example

You can see how I've implemented the Github Actions configuration through it's provided interface in Github:

## Conclusion

It is astonishing that people routinely accept the norm when there are better options available. How do you choose to invest your time? Personally speaking, I have better things to do than manually deploying code when I want to update my website and subsequently scrambling to fix things that break when my QE process was to blame. Imagine those that have to deal with this type of thing frequently and in their professional career. These "manual" approaches add up in terms of technical debt and required investment. As technologists, we need to be better and push to make the systems we build serve us too. Ultimately, it benefits those we're trying to serve by freeing us up to do better with the time and opportunity we have.