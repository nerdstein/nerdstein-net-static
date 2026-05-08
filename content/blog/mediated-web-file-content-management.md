---
title: "Mediated web file content management"
date: 2013-01-01
slug: "mediated-web-file-content-management"
tags: ["development", "drupal"]
description: "This is a topic I have grown all too familiar with, as this is my thesis topic for my master's degree."
draft: false
---

This is a topic I have grown all too familiar with, as this is my thesis topic for my master's degree. I thought I'd share some basics to set the stage in this area of work.

 

**Background**

Users upload files as content to web-based systems. Think of Facebook and how user's upload images and/or videos to share with friends. 

The key concept is around the notion of sharing. What is appropriate file sharing (anonymous access, authenticated access, membership-based access)? What is not appropriate sharing? This question changes based on application-level policy, meaning it's difficult to find a one-size-fits-all approach to solve this problem in every system.

It's not uncommon for a web system to use an unmediated file system. CDNs and standard OS file systems bypass application level mediation for files. If someone knows the URL to access a file, it will be served up to any user regardless of file sharing policies. This is common practice. So, how do we perform mediation on these files?

 

**Previous Work**

Some applications leverage token-based URLs in which a token provides a temporary capability to access the file. While this is fine, it doesn't necessarily respect the access control policy of the application. And, what happens if someone intercepts the capability?

 

**Design Challenges**

There is a missing level of semantics. Standard file systems are not aware of application-level operations. How does the file system know what policy to apply? Any file system needs some level of integration with the application itself to be effective.

Furthermore, application access control policies are not static. The classic example is when an employee is hired or leaves an organization. As such, the system needs to grant or restrict access appropriately. Any time the application adds/removes users or changes user-based permissions, the file mediation would need to be updated as well.

Another challenge is the process workflow of web requests. It's a series of handoffs. A request meets the OS with the web server port, which is passed off to the web server. The web server name resolution kicks in for the path of the request, which is passed off to either the specified server side script or the file asset directly on the file system. The only branch that performs mediation is the server-side script, typically during the application's name resolution bootstrapping process where the path is associated to some application-level resource. File assets are never mediated, as the application is never invoked.

 

**Mediation Considerations**

It's clear that some level of mediation is required to perform operations. But, what, where, how, and when?

What - One key thing to focus on is how to define proper file authentication. This is based on the application design and business logic found in the application. For example, Facebook users may only want to share with their friends. Google Plus users have the concept of circles, which is another abstraction on top just friends. Each application requires files to be sandboxed uniquely.  Understand the desired approach defined in the application policy and it should become clear what mediation should occur on file access.

Where - There are two principle points to evaluate: 1 - push mediation from the web server to the application, or 2 - educate the web server on how to properly authorize file access. I have opted to research the first way, simply due to my knowledge of web applications and not web server / operating system firewalls.

How - One must consider how to solve two problems: applying application-level semantics to web file assets and prohibiting unmediated access. To apply application-level semantics, one needs to extend the application to maintain mediation-specific semantics per file. There are many potential ways to solve this issue (file access control lists, custom database tables within the application, etc). And, in terms of prohibiting unmediated access, this can be solved with HTACCESS directives that instruct the web server to process these files differently.

When -  It's clear that mediation needs to occur when a file access occurs. The more complex part is identifying when to apply changes to the access control semantics. My advice is to take a look at the application framework itself. Application hooks may enable some level of integration based on events in the application. Such examples that affect access control would be events for user management, permission changes, or file management. 

 

**Challenges**

Blocking access to files (via a direct URL to the file) poses an issue in which the application must be responsible for rendering a file. This is no trivial task.

This also presents a usability concern. File rendering may change or alter the URL in which a file must be accessed (e.g. render-file?file=3). This URL link represents a radically different path than that in which the original filesystem-based URL exists. This can be solved by leaving files on the filesystem for file browsing and altering the HTACCESS approach to perform a redirect to a mediation script respecting the original file path. 

Ongoing maintenance of the application semantics is also tough. Any changes to the access control policy may require a full scan of the existing file content to ensure the policy is effectively performed. This advocates for more of a database-centric approach within the application that can run updates based on existing conditions contextually aware of the change to the application access control policy. 

 

**Feedback Welcomed**

I want to make sure my thesis is solid. Any contributions, comments, and/or ideas would be welcomed.