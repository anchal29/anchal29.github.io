---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 8
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the eighth week of the coding period of GSoC'16. The blogpost for the work done in the seventh week can be found [here][previous_blog].

This week I worked on providing test coverage for the module and fixed some issues. We decided to split the test into multiple classes which would extend one base class. This week I worked on this base class. We are using the entity_test provided by core's system module for testing purpose instead of any other ContentEntityType so that our tests could be as generic as possible (see [commit][commit1]).

As suggested by czigor we are using `\Drupal\Tests\BrowserTestBase` over `\Drupal\simpletest\WebTestBase` because the WebTestBase is provided by the simpletest module and they are not PHPUnit-based but built specially for Drupal and soon they will be deprecated (see [phpunit][phpunit]).

To create PHPUnit-based functional test we need to extend the `Drupal\Tests\BrowserTestBase`. Test class files should be at `my_module/tests/src/Functional/MyTest.php` and the namespace should be `Drupal\Tests\my_module\Functional`.

Recently in D7 we came across an issue with the deletion of revision of the parent entity which was causing site failure because we were trying to compare an entity with a NULL value using Diff module. This issue was also addressed for this branch by adding an extra column in our existing schema and then implementing `hook_entity_revision_delete()` (see [commit][commit2]).

So by the end of the week I made some progress with the base test class and also fixed an issue related with the parent_entity_revision_delete. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].


[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../11/GSoC-16-Port-Comment-Alter-Module-Week-7.html
[commit1]:https://github.com/anchal29/comment_alter/commit/d4e502afd17763791ece4ad778b9d8ada7f8b314
[commit2]:https://github.com/anchal29/comment_alter/commit/554f521c76124b346f2cf225bb1decf3ac94240b
[phpunit]:https://www.drupal.org/phpunit
