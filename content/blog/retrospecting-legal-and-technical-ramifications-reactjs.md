---
title: "Retrospecting on the Legal and Technical Ramifications of ReactJS"
date: 2017-10-31
slug: "retrospecting-legal-and-technical-ramifications-reactjs"
tags: ["development", "drupal"]
description: "Over the last few years, there have been substantial discussions around ReactJS, especially with regard to its former license."
draft: false
---

Over the last few years, there have been substantial discussions around ReactJS, especially with regard to its former license. This has little to do with the fact that ReactJS offers an attractive and innovative front-end development framework and that it has the backing of a major commercial entity. While I'm not an expert, the most controversial bits do not appear to be driven by copyright concern, but how their license applies to patents.

 

I've learned that legal and licensing can be a significant consideration in determining the technology we select on behalf of our clients, how combinations of technologies can be complicated by differences in licenses, and an acknowledgement of just how little I understand about these nuances and the associated risk. I wanted to write up my thoughts in retrospect, as Facebook has now changed the license for ReactJS. This post is a summary of what I learned as an engineer .

 

There were two articles that piqued my interest:

 

- [An explanation of potential motivations behind the licensing choices](https://medium.com/@ji/the-react-license-for-founders-and-ctos-b38d2538f3e5)

- [Wordpress’ decision to move away from ReactJS](https://ma.tt/2017/09/on-react-and-wordpress/)

 

Facebook originally opted to leverage a licensing strategy for the React open source project that aimed to protect themselves and their patents from future lawsuits. The primary concern that I understand is the ambiguity of what patents were bound to the license. While the patent grant applied only to patents related to ReactJS (of which, none are known), the patent retaliation clause applied to any Facebook patent, which included patents completely unrelated to ReactJS. This open-ended concern tied to this type of license left a lot up to interpretation and could potentially benefit Facebook legally in a much larger context outside of ReactJS itself (as described in the linked blog post “An explanation of potential motivations behind the licensing choices”). I find it shocking that adoption of an open source project could have such ramifications.

 

Ultimately, this ambiguity and lack of legal precedence in exploring limitations in this ambiguity presented unknown risks to those that chose to use ReactJS. I believe this ambiguity was intentional and motivated by a way to instill fear in future Facebook lawsuits based on their past patent-based lawsuits with Yahoo. But, Facebook included this licensing strategy under the guise of offering a cool and innovative open source project. I believe this went against the values of open source communities. Facebook could have chosen to clarify this by binding specific patents, but this doesn’t instill fear quite like something open ended.

 

This ambiguity is furthered by a lack of clarity in what specific patents were bound to React, if any. Facebook never explicitly defined which patents were involved. This introduces a number of specific technical implementations. What is a true definition of what is novel or unique about React itself? Is it the specifics of the framework? Is it the novel use of a virtual DOM? Such things may impact what Facebook is able to patent within React itself. But, this is not clear.

 

Some chose to move away from ReactJS in lieu of upgrading to the new version with a less threatening license. This may be wise, as there is nothing preventing Facebook from reverting the license back in future releases. There is still ambiguity of the best way to move off of the framework. Many people have approached this problem by leveraging a tool like Preact, which maintains a different implementation while preserves functional equivalence and parity with the ReactJS framework. Would this somehow violate any current or future patent Facebook maintains? Bear in mind, patents are based on ideas, not implementation. Due to the ambiguity, it’s not clear whether something like Preact would be covered by the same ReactJS patents. A safer replacement, but one that would require more refactoring would be Vue.js, which does not use the same framework and approach leveraged by ReactJS. But even in that case it is difficult to know since Facebook hasn’t specified which patent claims cover ReactJS. The Wordpress community found itself with such decisions of which frontend frameworks it would choose to support moving forward. I will certainly be following along and can appreciate the difficulty of not wasting community members time without being clear on the correct choice.

 

With so many unknowns, it is no wonder this became such a popular discussion topic for a framework rising in popularity and use. At a minimum, the optics of Facebook’s licensing strategy and the inherent ambiguity was highly suspect. It brings bad smells. Especially when open source is often associated with goodwill and communal interest. Often, people and companies will create distance based on optics alone. In this case, the optics directly correlated to unknown risks and is certainly enough for people to consider leveraging another comparable frontend framework, especially when performing new work and initial foundational architectural choices are being discussed. My main takeaway is to better explore the risks of selecting a framework from a legal (licensing) perspective and not just a technical perspective.