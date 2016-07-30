---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 7
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the seventh week of the coding period of GSoC'16. The blogpost for the work done in the sixth week can be found [here][previous_blog].

This week I worked on showing the differences made by a comment on the parent entity which involved using the Diff module. The differences are displayed only for parent entities supporting revisions (Node and Block Content in core). For the rest of the content entities comment alteration is supported but the differences are not shown.

Since we stored the old and new revision IDs along with the comment ID through which the parent entity was changed, we needed to compare the two revisions and display the differences on comment view.

+ At first I implemented `hook_ENTITY_TYPE_load()` for comments. It loads the old and new revision IDs of the parent entity for that particular comment from the DB and stores them in the `CommentInterface $comment` object.
+ After this I worked on `comment_alter_get_changed_fields()` which would return us a table showing the differences of the altered fields between the two revisions. This was achieved using the `EntityComparisonBase::compareRevision()` method of the Diff module.
+ Finally `hook_ENTITY_TYPE_view()` for comments was implemented which renders the table returned from the `comment_alter_get_changed_fields()`. I also added a stylesheet for the module.


By the end of the week we were able to display the differences on comments. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].


[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../04/GSoC'16-Port-Comment-Alter-Module-Week-6.html
