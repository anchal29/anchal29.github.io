---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 4
categories:
- blog
---

---
As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the fourth week of the coding period of GSoC'16. The blogpost for the work done in the third week can be found [here][previous_blog].

Fourth week of coding period has ended and this week I worked on completing the comment_form_alter() which is supposedly the toughest part of the comment_alter module. After implementing `hook_entity_extra_field_info()` last week, we needed to add field widgets for the pseudo fields added in the `hook_entity_extra_field_info()` implementation for the comment alterable fields.

Adding widgets for these fields could have been done either by adding them directly by specifying the type of the fields but that would lead to lots of validation checks or by getting the widget info directly from the parent entity. We are retrieving widgets information directly from the parent entity add/edit form. Earlier in D7 `field_attach_form()` was used for this and now we've used `entity_get_form_display()` and `EntityFormDisplayInterface::buildForm` for the same. (See [commit][commit1] and change record [#2225801][CR1].)

Now, the fields should be provided with proper weights retrieved from the comment display form but it turns out that we don't even need to set the weight of the added fields ourselves, it was taken care automatically for the corresponding fields. Further, all the necessary information which would be required later on were saved in the form element such as  alterable fields and their values. (See [commit][commit2].)

This also involved storing the column or sub-field information for any fields. Many fields have multiple sub-fields or columns like body field has "value" (the actual body), "summary" (the part that is usually displayed in the teaser) and "format" (the text format this field should be rendered with). Similarly, entity_reference fields stores "target_id" instead of values thus in order to tell if a field has changed or not in comment we are storing column information and value for all the alterable fields. (See [commit][commit3]).

By the end of the week I was able to complete the comment_form alter(). Now, we could see all comment alterable fields of the parent entity on the comment form with their default value as the one saved on parent entity. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].

[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../14/GSoC-16-Port-Comment-Alter-Module-Week-3.html
[commit1]:https://github.com/anchal29/comment_alter/commit/4911313c3164ee1f2c3f694d311838a3c7082696
[commit2]:https://github.com/anchal29/comment_alter/commit/4911313c3164ee1f2c3f694d311838a3c7082696
[commit3]:https://github.com/anchal29/comment_alter/commit/36dc9ffafe68a416b451c75d65a51e6acec7e887
[CR1]:https://www.drupal.org/node/2225801
