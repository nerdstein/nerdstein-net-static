---
title: "Balancing Theory and Practice"
date: 2016-09-23
slug: "balancing-theory-and-practice"
tags: ["development", "drupal", "people"]
description: "When you are building a tool, how do you measure the success of your efforts?"
draft: false
---

When you are building a tool, how do you measure the success of your efforts? There are data driven approaches around adoption, like number of times your tool has been downloaded or installed. Similarly, success could be defined as how effectively you solved the problem. This could be measured by the number of issues filed, the (hopefully) lack of vulnerabilities, or the number of feature requests created. But, in any measure, success is actually defined by **other people**. And, as an engineer, it's such a difficult task to put yourself in their shoes. How do you deal with that?

## Theory

People are not purely logical. Analytical minds are. Computers are. Your theory may be sound, but the product you build could receive negativity from people. This often means that people acknowledge the potential benefit (they tried it, right?) but there is something that doesn't meet their **practical** needs.

Let's look at why:

- **Usability** - A technically sound and useful tool exists, but there is limited documentation on how to use it, the tool is confusing to use, or too cumbersome to use effectively.

- **You didn't solve the problem completely** - People expected different outcomes or more functionality than the tool provides.

- **You assumed targeted use** - There are other use cases individuals need that you didn't account for or didn't provide any ability to resolve.

## Practice

How do you make things more practically useful?

- **Listening** - Those that use your tool will engage you in conversation. Be prepared for it and actually listen. You developed something you are likely proud of, but put it aside and try to be open to hearing about how people feel about what you've done. Even the goodwill and means in which you articulate your thoughts will help build allies.

- **Extensibility** - It's impossible to catch all of the ways and means someone may want to use your tool. As such, prioritize ways that others can extend or adjust the behaviors. In Drupal terms, use hooks, events, and plugin systems.

- **Interoperability** - A common trap is to just assume your tool is to be used by one system in defined use cases. Evaluate the opportunities for your tool to interact with any system regardless of platform or framework.

- **Pragmatism** - Common sense reminders: please organize your code into logical and reusable parts, provide documentation, leverage coding standards, avoid complexity, and have peer reviews to validate all of this. Those that use your tool will have more confidence that the developer is not merely hacking something together.

- **Automated testing** - As your tool evolves, build a robust suite of automated tests to limit breakage and ensure those using the tool are not surprised.

## Conclusion

> Dialogue is born when I am capable of recognizing others as a gift of God and accept they have something to tell me. - Pope Francis

It's not easy doing this kind of work. It's much harder when walls are built between community and those building a tool. Find ways to engage people throughout development and maintenance. You'll watch your idea flourish by engaging in dialog for diverse ideas and perspectives. Such a philosophy applies practicality to theory.