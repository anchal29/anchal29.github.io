---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 10
comments: true
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the tenth week of the coding period of GSoC'16. The blogpost for the work done in the ninth week can be found [here][previous_blog].

Since I was almost done with the base test class last week, this week I mainly focused on providing test cases for different fields and widget types. Also I added tests to the base class to check that the module is not breaking anything on a revision delete. I started this week by extending the tests for text fields which I completed last week to cover multi-valued text field altering. Then I added tests for list(string) fields which included several widget types like select list, checkboxes and radio buttons.

Later this week I added tests to check if the `hook_entity_revision_delete()` was working as intended, i.e. the module was not breaking anything in case a revision of the parent entity was deleted. After this I added tests for image fields and while doing this I came across an issue with multi-valued image/file fields which I corrected and it is working fine now, without breaking anything else.

* * *

Executing the automated tests
=======

The module has PHPUnit tests and it is recommended to execute the unit tests using command line instead of the web interface provided by the SimpleTest module. More instructions can be found [on the related drupal.org documentation page][1]. Executing these web tests:
{% highlight ruby %}
cd /path/to/drupal-8/core
export SIMPLETEST_DB=mysql://drupal-8:password@localhost/drupal-8
export SIMPLETEST_BASE_URL=http://drupal-8.localhost
../vendor/bin/phpunit --group comment_alter
{% endhighlight %}

When the user executing these functional tests is different than the one running the web server (apache for example), an exception is thrown and it’s not very clear what the problem is. Running these tests as root or changing permissions of files doesn’t have any effect on it. The recommended approach here is to change the user running the web server to the system user.
Other way is to run these tests with the same user as the one running the web server, this can be achieved by using this command instead (see [#2760905][2760905]):
{% highlight ruby %}
sudo -u apache ../vendor/bin/phpunit --group comment_alter
{% endhighlight %}

To execute any single test or a class the `--filter` tag can be used. Example: if we just want to run `testOptionsSelectSingle` then following command will do so:
{% highlight ruby %}
../vendor/bin/phpunit --group comment_alter --filter testOptionsSelectSingle
{% endhighlight %}

* * *

By the end of the week I completed tests for single and multi-valued text, list(string) and image fields. As of now the module is passing all the tests and there are no known issues. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].


[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../../07/26/GSoC-16-Port-Comment-Alter-Module-Week-9.html
[2760905]:https://www.drupal.org/node/2760905
[1]:https://www.drupal.org/node/2116263
