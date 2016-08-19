---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 12
comments: true
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting [Comment Alter][] module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the twelfth week of the coding period of GSoC'16. The blogpost for the work done in the eleventh week can be found [here][previous_blog].

The GSoC coding period ends this week and I’m glad that I was able to complete the project as per my proposal. All these three months have been very productive for me during which I learned a ton of things not just related to Drupal but also things like writing blogs, managing the project, etc.

During the coding period being stuck on a problem for 3-4 days and after countless hours of debugging finding the solution to be a one-liner or getting good reviews from mentors were some of the most intriguing and satisfying moments for me. I would like to thank both of my mentors [boobaa][] and [czigor][] for always helping me with coding, blogs and project management. It would have never been possible without them. I would also like to thank the whole Drupal community  and Google Summer of Code for providing this opportunity to me.

Now talking about the work which I did this week, since most of the coding part was completed last week this week I focused on adding documentation for the module, doing cleaning and proof reading of the whole repo. I’ve created a short demo video: [Comment Alter module for Drupal 8][screencast] demonstrating a simple use case and working of the module.

<iframe width="630" height="315" src="https://www.youtube.com/embed/9ZJqlbrPwxY" frameborder="0" allowfullscreen></iframe><br />

This week I also fixed some minor issues like changing the `#parent` property for the comment form for all the fields to avoid any clashes. In order to allow same name fields on both comment as well as parent entity the `#parent` property was used in the `comment_alter_form_comment_form_alter()` function. Due to this the submitted field values appeared at a different location preventing instances of multiple field value in the same `#parent` space or `$form` element (see [commit][]).

In the upcoming week I would first move the module to [drupal.org][d.o.] and will update the description about the module on the project page. I planned to move the module to drupal.org last week only but because of some complications, my mentors were unable to do the final review of the module. My mentors will do with the review before this Friday so I’ll move the module to drupal.org by then.

By the end of the week I’ve created a demo video for the module and fixed some issues. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed on my [GitHub repo][github_repo].


[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../08/GSoC-16-Port-Comment-Alter-Module-Week-11.html
[d.o.]:https://www.drupal.org/
[commit]:https://github.com/anchal29/comment_alter/commit/161cf5ea9671d6772d8963610d1b7cc359c8ebe2
[screencast]:https://www.youtube.com/watch?v=9ZJqlbrPwxY
[Comment Alter]:https://www.drupal.org/project/comment_alter
