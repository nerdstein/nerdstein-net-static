---
title: "Getting Started with Drupal Rector Development"
date: 2020-05-05
slug: "getting-started-drupal-rector-development"
tags: ["development", "drupal"]
description: "Drupal 8 introduced a lot of changes. Its usage of best-of-breed dependencies, like Symfony, represented a major shift for Drupal."
draft: false
---

Drupal 8 introduced a lot of changes. Its usage of best-of-breed dependencies, like Symfony, represented a major shift for Drupal. Drupal 8 also moved to a more nimble release cycle with its major and minor releases, allowing a major version of core to get new features in minor releases. Between dependencies releasing updates and changes to core being more common, Drupal needed to evolve to manage change. One way this happens is through deprecations. This provides a way for Drupal to evolve, identify old code as deprecated, and offer guidance on a replacement. Deprecations were especially common as Drupal evolved from a largely procedural approach to one leveraging more object orientation and some of the design patterns Symfony uses, like controllers, services, and more. But, the great thing about this approach for deprecations is that deprecations do not get removed until the next major release of Drupal. This buys the community time to progressively fix deprecations within their code and is somewhat expected between major releases. But, what if addressing deprecations could be automated?

 

Rector, in its simplest format, is an automated, fancier "find and replace" tool for deprecations. It tries to identify the correct symbols and conditions to perform substitution within a library of rules. Each rule has two primary parts: what it is seeking to replace (statement, method, function, argument, and more, represented as a class) and a processing method to perform the replacement. Each rule returns the object with the proper replacement. This processing is great for nuances tied to deprecations, like optional arguments. Rector’s underlying tooling has fine-grained symbolic control that allows for the highest degree of tuning around deprecations.

 

Did you know that Drupal is able to automate updating deprecated code? Did you know that these updates represent the bulk of the code development work required to upgrade from Drupal 8 and 9? Did you know that this approach works for core, contributed projects, and for custom code? And your help is needed.

 

This blog post demonstrates how to create and run Rector rules, with some tips along the way. If we all paused from our hectic lives and made just one Rector rule, we could hit a really high percentage of refactoring (note: it may be impossible today to do this kind of automation and hit a flawless 100%). The future goal of this should be upfront time savings with a follow-up manual review and testing to ensure the automation worked.

 

## Background

In my undergrad, we learned about compilers, particularly Lex and Yacc. In grad school, we leveraged symbolic execution for vulnerability analysis. I didn’t find either experience all that satisfying. Both represent a broader umbrella of symbolic computing, with different intended purposes. In short, the code in programming languages can be broken down into its smallest, atomic parts, line by line, part by part.

 

Let’s break down a simple statement, *$number = 8;*. A variable in PHP starts with a "$" character and the context of the variable can change based on the location of a variable. The "=" sign refers to the assignment operator, where the variable set is to the left of the equals sign. "8" represents a literal value, not generated like a function. All of this is considered a statement, which is terminated with a ";" character.

 

The key takeaway is that even a line of code that is trivial to type is a series of symbols with specific semantic meaning tied to the program language itself. Now, imagine expanding this into conditions, functions, objects, and much more.

 

## Getting Started with Drupal Rector Development

These steps should serve as a high-level walkthrough to getting started. Development best practices are still being established, and I encourage joining the #rector Slack channel on drupal.slack.com to get help, offer feedback, and coordinate contribution.

 

### Step 1: Getting setup

The Palantir.net team has set up [a sandbox project](https://github.com/palantirnet/drupal-rector-sandbox) with instructions on how to rapidly set up an environment for Drupal Rector development. The development instructions follow most Github standards, where a fork of the Drupal Rector project is created to observe the standard pull request workflow.

 

To identify a deprecation to work on, check the consolidated list of deprecation notices in public modules [here](https://dev.acquia.com/drupal9/deprecation_status/errors) (filter by category "not covered by rector" and click on the "total occurrences" column for a sense of impact). Mention the deprecation on the rector channel on Drupal slack for discussion and check that someone hasn’t already filed the issue on [the drupal.org issue queue](https://www.drupal.org/project/rector). If no one has worked on it, file an issue in the [issue queue](https://www.drupal.org/project/issues/rector) and assign it to yourself for the unassigned deprecation you wish to work on.

 

### Step 2: Mock up code and analyze

It is important for you to mock up code examples for all variations that demonstrate both the old (has deprecations) and the new (remediated) code. Yes, **you should do both**. Why? Drupal Rector dependencies ship with an analysis tool that shows you how statements are composed. It breaks down a statement into a hierarchy of parts. Running the analysis tool against the old and new code helps you identify differences.

 

A specific example file for *Drupal::url* can be found [here](https://github.com/palantirnet/drupal-rector/blob/master/rector_examples/src/DrupalURLStatic.php), found in a file named *DrupalURLStatic.php*. To run the analysis tool against that file, as an example:

> vendor/bin/php-parse web/modules/custom/rector_examples/src/DrupalURLStatic.php

###

### Step 3: Develop the Rector Rule

#### 3.a. Creating the Rule

Create a new rector rule class within [this directory](https://github.com/palantirnet/drupal-rector/tree/master/src/Rector/Deprecation). Check [existing base classes](https://github.com/palantirnet/drupal-rector/tree/master/src/Rector/Deprecation/Base) for some helpful starting points that will simplify the logic within your rule. When possible, extend a base class, otherwise, extend the *AbstractRector* class from the Rector utility. Please bear in mind that if a base class exists, this likely automates a lot of the processing. You may not need to follow every step defined below, but I capture the basic steps you need without a base class.

 

Begin with a *getDefinition()* method that provides a human readable description and simple before and after code sample.

 

Next, create a *getNodeTypes()* method. Running the analysis tool in step 2 against both the old and new code samples offer guidance on how to create the remediated code returned from the processing in the rule. The generated output of the analysis tool will help highlight exactly what development changes are required to get an old code sample to become the new one. For efficiency and best practice, your starting point should be the highest order difference between the old and new code. Are you replacing a whole statement? Are you replacing a function or just an argument? Within this function, return an array of matching class types tied to the highest order class. This will send all instances of this class as an argument to your processing function when the Rector engine executes. Classes are represented as one or more PHPParser *node* class types. Please note, this is not a Drupal node, but a PHPParser base class representing the breakdown of the PHP language (e.g. functions, objects, statements, etc).

 

Finally, create the processor by creating a *refactor(Node $node)* method. It’s common in this method to further refine the conditions of the passed argument. For instance, if you pass a deprecated class method like *getEntity*, the argument will receive a class of type *ClassMethod*. A simple condition to check the name attribute of this instance will refine the processing further.

 

Proceed to create the new desired code hierarchy in the refactor method from the differences between the code samples. As an example, if you only need to change the name of a method, replace the name attribute in the passed argument and return the object at the end of the processing. Processing differences can be drastically more complex, but encouraging the use of base classes and patterns should lower the complexity over time.

 

*An example of a Rector rule*

#### 3.b. Register the Rule

Rules should be associated with a deprecation. A deprecation associates to an issue that identifies what major/minor version of core that introduced the deprecation. Any rules that are created from the deprecation need to be registered in the correct config file found in this directory. If there is not an associated config file for the major/minor version, create a new YAML file with the class name for the rule. Add this new YAML file to [the project’s YAML file](https://github.com/palantirnet/drupal-rector/blob/master/rector.yml) and the new YAML file referenced in the ['all deprecations' YAML file](https://github.com/palantirnet/drupal-rector/blob/master/config/drupal-8/drupal-8-all-deprecations.yml).

 

*The rector.yml configuration file*

*An example configuration file that registers a Rector rule*

### Step 4: Running and Validating

Double check your YAML configuration to ensure the rules are properly registered.

 

To see a dry run of the rector engine processing, use the following to process all of the rector examples:

> vendor/bin/rector process web/modules/custom/rector_examples --dry-run

 

This will help to debug and iterate on your new rector rule. Running this command will display code that matches Rector rules and code that does not. Hopefully the matches are the old code that needs to be updated to the new code. The new code should come back clean.

 

*A partial example of a log output*

Remove the *--dry-run* flag and replace the path to actual code to have Drupal’s rector engine perform code refactoring.

 

## Summary

Automating deprecations can be complex but it is high impact work. It should become our new muscle memory as we continue to deprecate code in the future. Imagine handing developers a tool capable of automatically performing maintenance to code indefinitely. We can get there.

 

I want to thank the following people for reviewing and contributing to this blog post: Dan Montgomery, Ofer Shaal, Ken Rickard, Dries Buytaert, Gabor Hojtsy.