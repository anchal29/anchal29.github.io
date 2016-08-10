---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 3
comments: true
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the third week of the coding period of GSoC'16. The blogpost for the work done in the second week can be found [here][previous_blog].

Since I was done with [get_alterable_fields_function()][1] last week, this week I started working on comment form alter. My mentors suggested me to port `comment_alter_field_extra_fields()` function first, which would add pseudo fields on comment_form for these extra comment_alterable_fields before adding widgets for these fields on the comment_form to expose some control over this to the UI. It would allow sitebuilders to re-order all the comment fields and the comment_alterable_fields. Also this function adds one extra pseudo field on comment_display so as to render the parent entity field changes for the comment in any particular place decided by the sitebuilder.

> Pseudo fields are simple display/form fields whose position can be controlled from the display settings of a particular entity type. An example of such a field is the core Links field on the node or comment entities. This allows us to add extra fields for a particular entity which can be reordered.

For more information related to pseudo fields, I would recommend looking at [hook_entity_extra_field_info()][2] and also I came across this [article][] which was helpful to me. This [commit][3] implements `hook_entity_extra_field_info()`.

There were some major changes from D7 to D8 which affected the port of this function.The most important thing was that in D7 we had separate comment types for all content types so it was relatively easy to attach the extra fields of that particular content type to the comment. In D8 however any comment type can be attached to any entity type so we cannot know what extra fields we need o attach to the comment. (See change records [#2100015][4] and [#2285633][5].)

So, in order to attach the extra comment_alterable_fields of the parent entity to its comment types, we need to loop through all the comment types attached to our parent entity (as we may have more than one). I had some problem getting the comment bundle information of the comment fields attached to the parent entity which I later found in the `FieldStorageDefinitions`. Basically we wanted to know the comment bundle of the comment field attached to our parent entity but instead it was in `FieldStorageDefinitions`. (See [commit][6].)

By the end of the week I was able to implement hook_entity_extra_field_info(). Now I have extra fields in my comment_type _form and _display which I can drag around using the UI. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].

[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../07/GSoC-16-Port-Comment-Alter-Module-Week-2.html
[1]:https://github.com/anchal29/comment_alter/commit/1b12cfceac23afce40349d02ebb4a4c705282c89
[2]:https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Entity!entity.api.php/function/hook_entity_extra_field_info/8.2.x
[article]:https://www.webomelette.com/creating-pseudo-fields-drupal-8
[3]:https://github.com/anchal29/comment_alter/commit/2458eaf72172a933f89448a39bcd911349fee2a1
[4]:https://www.drupal.org/node/2100015
[5]:https://www.drupal.org/node/2285633
[6]:https://github.com/anchal29/comment_alter/commit/859bdc76e1c84b74e7ca54006971ffd8af1f2e63
