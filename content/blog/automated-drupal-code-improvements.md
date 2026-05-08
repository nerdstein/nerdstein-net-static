---
title: "Automated Drupal Code Improvements"
date: 2013-01-01
slug: "automated-drupal-code-improvements"
tags: ["development", "drupal"]
description: "The Coder module (http://drupal.org/project/coder) is well known for assisting developers in producing code up to snuff with the community defined standards."
draft: false
---

The Coder module ([http://drupal.org/project/coder](https://drupal.org/project/coder)) is well known for assisting developers in producing code up to snuff with the community defined standards. Such standards have been integral in helping the community grow in a consistent manner.

The ultimate goal is to find an automated way to help developers out. Such examples include a ***code review ***and performing routine ***code manipulation.*** The standard for analyzing code leverages known ***static analysis*** approaches. There are two principle goals for code: ***consistency*** and ***simplicity***. 

 

**Consistency**

To understand what consistent code looks like, we need to understand Drupal itself. Drupal has ***APIs*** that are intended to provide consistency for events (the hook system) and core functionality (functions and libraries of code). Consistent code can then be viewed as code that properly leverages the APIs. For example, someone who doesn't understand the Database API may be inclined to use PHP's native *mysql_query* function. Use of this function would not be consistent with other Drupal modules.

Additionally, the Drupal community has adopted ***development standards*** (see: [https://drupal.org/coding-standards](https://drupal.org/coding-standards)). This defines how code should be formatted, documented, etc. Participating in such standards welcomes community involvement and makes your code more readable to others who leverage Drupal.

 

**Simplicity**

One of my favorite presentations from DrupalCon Denver was "Development By The Numbers" ([https://portland2013.drupal.org/session/development-numbers](https://portland2013.drupal.org/session/development-numbers)). During this presentation, Anthony Ferrara demonstrates metrics for evaluating code complexity. His main claim is that limiting complexity increases quality (and, in this case, simplicity). 

Complexity can be measured in a number of different ways (seriously, check out the slides). One of the more well-known metrics is ***cyclomatic complexity*** which statically analyzes code to find methods/functions with a high number of potential branches. This is a useful metric for identifying code that would be difficult to test. If code is difficult to test, its even more difficult to guarantee correctness. Complex code then becomes prime candidates for ***refactoring***.

 

**Solutions**

While Coder has some really nice tools to use within Drupal itself, I believe some of it's most powerful features happen with Drush. Drush commands can then be integrated into a development workflow within a continuous integration solution. Let's consider the following:

 

```

drush coder-format <custom module name here>
```
This is a slick one liner to *consistently* format all code in a module. Boom! John Madden style.

 

```

drush coder-review <custom module name here>
```
Again, another slick one liner to identify improper use of Drupal's APIs and a myriad of other things to ensure *consistency*.

 

```

drush coder <custom module name here> --sniffer
```
By running that command, this returns the cyclomatic complexity of a module to analyze *simplicity* (enabled by this patch: [https://drupal.org/node/1934594#comment-7171972](https://drupal.org/node/1934594#comment-7171972)). Note: Ferrara also mentions the command line tool PHPLOC as an option.

 

 

While some may argue about the ways and means of making code more consistent and simplistic, few could disagree with the benefits of doing so. Hopefully this post shed some light into some potential automated means of solving these challenges.

 

 

 

References:

[http://deeson-online.co.uk/labs/drupal-cyclomatic-complexity](http://deeson-online.co.uk/labs/drupal-cyclomatic-complexity)

[https://github.com/sebastianbergmann/phploc](https://github.com/sebastianbergmann/phploc)

[http://pear.php.net/package/PHP_CodeSniffer/](http://pear.php.net/package/PHP_CodeSniffer/)

[https://drupal.org/node/1419988](https://drupal.org/node/1419988)