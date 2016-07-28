---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 6
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the sixth week of the coding period of GSoC'16. The blogpost for the work done in the fifth week can be found [here][previous_blog].

Last week I worked on the submit and validate callback functions but in the submit function only the parent entity was stored. In order to show the changes made by a comment we need to create new revision of the parent entity and store the revision ID corresponding to that comment. A revision can be created using `setNewRevision` if the entity supports revisions. In case if entity is an instance of [RevisionLogInterface][1] we also set the revision_user_id and the creation time. (For e.g. See [NodeForm::submitForm()][2]).

There are some content entity type which doesn’t support revisions like the taxonomy term. For those entity we decided to allow altering of the comment alterable fields from the comment form. Though the changes made by a particular comment wouldn’t be available then as we are using revision for this.
Later this week I tried to fix following issues related to the field widgets:

1. **Multi-valued fields add more option**: One of the issue was add_more option of any multi-valued field widget. Clicking the add_more button was resulting in an AJAX error and we were unable to add any extra fields to a multi-valued field. Fix to the issue was rather small, just removing the `comment_alter_` prefix from the alterable field names solved this issue.(See [commit][3])

2. **Checkboxes/radio buttons and select list widget**: In case when checkboxes were used as a field widget, `Element::children()` was giving a fatal error as there were no any children elements in the `$form[$alterable_field][‘widget’]` element. So, to fix this we needed to bail out early or get the column information from the `#key_column` property of the form element.

By the end of the week I was able to complete the `comment_alter_form_comment_form_alter_submit()` function and fixed some of the issues related to field widgets. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].

[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../../06/28/GSoC'16-Port-Comment-Alter-Module-Week-5.html
[1]:https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Entity!RevisionableInterface.php/function/RevisionableInterface%3A%3AsetNewRevision/8.2.x
[2]:https://api.drupal.org/api/drupal/core%21modules%21node%21src%21NodeForm.php/function/NodeForm%3A%3AsubmitForm/8.2.x
[3]:https://github.com/anchal29/comment_alter/commit/f0965b87b3ea7fbfdfff7b69510107e0dba3a6b7
