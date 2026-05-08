---
title: "Simpletests hanging in Drupal 8?"
date: 2015-07-18
slug: "simpletests-hanging-drupal-8"
tags: ["development", "drupal"]
description: "I recently had a difficult situation in which I could not debug a hanging Simpletest in Drupal 8."
draft: false
---

I recently had a difficult situation in which I could not debug a hanging Simpletest in Drupal 8. Before continuing on, **add the *dblog* module as a dependency to the Simpletest** you are writing and rerun it. **Your test may be hanging because it cannot write to the error log.** If it continues to hang, read on.

 

## Hanging test with no output

When a test hangs, there are no signs of life. It leverages Drupal's Batch API. The screen just sits on a progress bar of death. This process continues to run indefinitely and then causes performance issues. 

 

When running the test, it will never leave the batch screen. There will be no support messaging and the URL will look something like this:

 

> *http://d8.dev/batch?id=13&op=start*

 

So, what do you do?

 

## Off to the command line!

Don't be scared. You can often see a bit more output by running it from the command line and not from the interface. There are two ways I primarily do this: by module or by class. Both are run from your Drupal 8 docroot.

 

Module: *php core/scripts/run-tests.sh --verbose --url [http://d8.dev/](https://d8.dev/) --color password_policy*

Class: *php core/scripts/run-tests.sh --verbose --url [http://d8.dev/](https://d8.dev/) --color --class "Drupal\password_policy\Tests\PasswordResetBehaviors"*

 

This is often really good for debugging fatal errors. I still prefer the interface to retrieve the screenshots when debugging a working, but failing simpletest.

 

## Next, the database!

First, **do not clean the results**! These are your artifacts from the last testing run. You can follow these steps to get the test output.

 

- Get into MySQL via the command line, Sequel Pro, or your MySQL tool of choice

- Run the following query:
*select * from simpletest;*


- Audit the rows returned, paying careful attention to the *test_id* field, the highest value represents the last tests you ran

- For a visual, look for rows that show "*Verbose message*". You will find a URL, which you can copy and paste into your browser for a screenshot of Drupal.

 

This provides you access to the same output after running a Simpletest, in the case that your output is not returned from a test that hangs. After auditing the MySQL rows and debugging, clean out existing tests to ensure you do not run into performance problems before running additional tests.

 

## Fatal error with no output

You may see that the last row states "*Fatal error*" and leaves no further details. You check your standard apache error log, no dice. So, where do you get more information?

 

When invoking Simpletest, Drupal creates it's own multisite for it. It's logs reside under the site, found in */sites/simpletest.*  You will see subdirectories for each test. Match up the *test_id* column from the fatal error row to get the associating test subdirectory. Inside of the subdirectory, you will find error.log. These usually end up being the same PHP errors you would typically find when auditing apache error logs.