---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 5
comments: true
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the fifth week of the coding period of GSoC'16. The blogpost for the work done in the fourth week can be found [here][previous_blog].

This week I started working on submit callback function of the altered comment form which should save the changes made on the parent entity's alterable fields present on our comment form. We can't directly change these values in parent entity from our comment form so there was a nice trick to it. Build the entity display form again and then set the values of alterable fields in it from the comment form and then save the parent entity display form. So this way when submit function is called comment will be save and also our parent entity will be edited. (See [commit][1]).

After this I worked on validation callback and in similar manner i.e. by creating parent entity display form again and copying values of the comment form, validation for the form was done using [EntityFormDisplayInterface::validateFormValues()][2]. After completing this again I moved back to complete our submit callback function through which we are able to alter fields of parent entity from comment form.

In order to show those changes we need to create revisions and to save CPU cycles and memory we need to save data only if there was some change in the alterable field entities. So as next step I made sure that anything was saved only if there were some changes in the alterable fields which required to clean up comment form alterable field values and old values to remove any non alterable columns from them. (See [commit][3]).

By the end of the week I was able to complete the validate and submit function but there are still some issues with submit callback function which needs to be rectified before we proceed further. So, I would like to work on them this week. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].

[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../20/GSoC-16-Port-Comment-Alter-Module-Week-4.html
[1]:https://github.com/anchal29/comment_alter/commit/5a1a91c62e4259c26f0205a0a1a2a5e349619b4e
[2]:https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Entity%21Display%21EntityFormDisplayInterface.php/function/EntityFormDisplayInterface%3A%3AvalidateFormValues/8.2.x
[3]:https://github.com/anchal29/comment_alter/commit/bbc6f7ac240642f53a8a4caea260c7249bc0668d
