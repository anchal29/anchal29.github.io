---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 9
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the ninth week of the coding period of GSoC'16. The blogpost for the work done in the eighth week can be found [here][previous_blog].

This week I continued to work on providing test coverage for the module. Last week we decided to use `EntityTest` as our parent entity and check the functionality of the module over it but while writing tests I came to know that it didn’t support revisions. To write tests using revisionable entities we have to use `EntityTestRev`.

While using `EntityTestRev` entity I came across an issue: our alterable fields were not shown on the comment form. However, earlier when I used `EntityTest` it was displayed correctly and even the values got altered. It did not display the difference since it did not support revisions. I was stuck here for quite a while figuring out what the real problem was.

It turned out that it was a problem with cache invalidation. Field UI was disabled for the `EntityTestRev` entity thus the `comment_alter_field_config_edit_form_alter()` was not called, inside which the cache was deleted. Adding the following lines did the trick for me instead of having Field UI enabled for the parent entity.
{% highlight ruby %}
    \Drupal::cache()->delete('comment_alter_fields:' . $this->entityType . ':' . $this->bundle);
{% endhighlight %}


After resolving this problem the test was working fine and the differences made from a comment were displayed. Later I worked on the `assertCommentDiff()` function which tested the differences displayed over the comment-alter-diff table were expected. For now we have tests for Text Field and I’ll cover other field types by next week (see [commit][commit1]).

So by the end of the week I completed the function `assertCommentDiff()` and tested it for single valued text fields. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].


[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../19/GSoC-16-Port-Comment-Alter-Module-Week-8.html
[commit1]:https://github.com/anchal29/comment_alter/commit/92639c8a9e3405cf98fe75b640815e0a561e5a15
