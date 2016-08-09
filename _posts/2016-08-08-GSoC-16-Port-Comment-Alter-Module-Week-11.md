---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 11
comments: true
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the eleventh week of the coding period of GSoC'16. The blogpost for the work done in the tenth week can be found [here][previous_blog].

In D7 the comment settings were present on the node and those settings were managed from node edit forms whereas in D8 comments settings became fields and they could be attached to any other entity type (see change record [#2100015][]). In D7 version of the module all the comment related settings were present on that comment settings section of the node type edit/add form. So in D8 we could have added those settings to either the entity_type edit form or to the comment fields and we decided to go with the later one. This week I added all these settings and their implementations along with the tests for them (see [commit1][] and [commit2][]).

During our weekly stand-up this week we had following discussions:

* Both of my mentors are going to do a final review of the whole code and after all the corrections hopefully the module can be pushed to d.o. I’ve been provided with the required permissions to do so.
* I’ll be creating a demo video this week. The demo video will cover comment_altering of node fields and it will cover all the comment related settings which governs working of the module.
* Since the deadline of the final submission of our GSoC project is 23rd Aug we had a discussion about the final submission. Based on the [Work Product Submission Guidelines][], [boobaa][] suggested me to do the following two things:
    1. Prepare a blog post describing all the work which I did and what is left in that and why.
    2. The link to the github repo on which I worked throughout this project. Also we will have the d.o. repo of the module.

Last week I added tests for most of the field types but as suggested by my mentors this week I also added tests for Entity Reference fields (see [commit][commit3]). As of now the module is working on Drupal 8.2.x and all the tests are also passing. Once the final review of the module is done we plan to push the code to d.o.

By the end of the week I completed tests for node reference fields and added comment_alter related settings and also added tests for them. For now I’ll work on adding documentation for the module. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].


[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../03/GSoC-16-Port-Comment-Alter-Module-Week-10.html
[#2100015]:https://www.drupal.org/node/2100015
[commit1]:https://github.com/anchal29/comment_alter/commit/80e04efb6b73983d4eb7bbeb8d09e6be6eea4034
[commit2]:https://github.com/anchal29/comment_alter/commit/d3083a50c85848efb3ab5d426433f90348fd0794
[Work Product Submission Guidelines]:https://developers.google.com/open-source/gsoc/help/work-product
[commit3]:https://github.com/anchal29/comment_alter/commit/552e6a512a7c597191daa0c9ccef9856875ce52e
