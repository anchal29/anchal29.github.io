---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 1
comments: true
categories:
- blog
---

---

The coding period for GSoC 2016 started last week from 23rd May and now students are required to start coding for their respective projects. As part of GSoC'16 I have been working on **Porting Comment Alter module to Drupal 8** under mentorship of [boobaa][] and [czigor][].

The first week of GSoC'16 coding period is over now. During this week I was able to accomplish following tasks:

+ **Creating schema for the module**: I started out with preparing the schema for the module and created the .install file which implemented hook_schema to store comment ID, old and new revision ID for the parent entity. As pointed out by [boobaa][], storing the comment ID provided us with the flexibility of leaving out some column from database schema of the module. We can find the parent entity type and entity ID from comment table using the comment ID stored.
+ **Creating a form_alter for settings screen**: After writing schema for the module, I worked on the first function of our module which implements `hook_form_FORM_ID_alter`. This provides an interface to select any field we want to be altered by the comment and also hide alteration from diff. So by using the `hook_form_FORM_ID_alter` we could add these extra options on the field_config_edit_form but there was a change from the D7 version here. Earlier additional field properties were directly stored in the database just with the addition of those custom fields in the form_alter but now we need to use `ThirdPartySettings` to store the values.
+ **Using ThirdPartySettings for storing form_altered values**: I was stuck here for a while. I went through some of the issues and blogs related to `ThirdPartySettings`. Content_translation module in core was a good example which used ThirdPartySettings and it even also implemented `hook_form_FORM_ID_alter` for field_config_edit_form. There were two methods by which we could have used `ThirdPartySettings` in our module. The one we are using was to use the `ThirdPartySettingsInterface` provided for `FieldConfigInterface`. The other one was to create our own builder function. We are not using the other method because it will increase the complexity as we would have to add our own builder function inside which we would set the `ThirdPartySettings` to store our changes. But it would be independent and will not be affected if any other module also uses ThirdPartySettings.

Finally with the use of `ThirdPartySettings` we have completed our first function which provides an altered `FieldConfigInterface`. My mentors have already reviewed the code for the work which I did in this week. If anyone is interested, my progress can be followed [here][github_repo].

[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
