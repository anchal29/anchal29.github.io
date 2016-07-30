---
layout: post
title: GSoC'16 - Port Comment Alter Module - Week 2
categories:
- blog
---

---

As part of GSoC'16 I'm working on **Porting Comment Alter module to Drupal 8** under the mentorship of [boobaa][] and [czigor][]. This blog is an excerpt of the work which I did in the second week of the coding period of GSoC'16. The blogpost for the work done in the first week can be found [here][previous_blog].

The second week of GSoC'16 coding period is over now. During this week I was able to accomplish following tasks:

1. **Make sure that a comment alterable field of parent entity is not present in comment form**: Now, in Drupal 8 this problem can arise only in one case i.e. when comment is parent entity because now fields are not shared across entity types only across the bundles of a given entity type. As upon discussion with my mentors we concluded that to avoid any unnecessary complications we would remove comment altering options from comment fields which would resolve this problem. This means comment fields can not be altered from comments now, which also doesn't serve us any purpose.
2. **Get comment alterable fields**: After providing options to make a field comment alterable and making sure that parent entities fields are not present in comment, I started to work on a function which would return all the comment alterable fields attached to the parent entity. This required getting the `ThirdPartySettings` stored previously to check whether a field is comment alterable or not using the field definition. Also in the meantime I was able to learn about caching in Drupal specially about cache invalidation on which I did some mistakes in the beginning. Now, the function works and I'm able to get all the comment alterable fields attached to an entity.
3. **Porting comment_alter_form_node_type_form_alter function**: Procedural next step for me this week was to work on porting this function of Drupal 7 as it would affect the comment form. For now I provided this form alter for comment fields settings which needs to be moved to entity edit form.

By the end of the week, with this I was able to get the list of the comment alterable fields attached to parent entity. Adding the field widgets for the comment alterable fields in the comment form would be the next step for me. My mentors have already reviewed the code for the work which I did during this week. If anyone is interested, my progress can be followed in my [GitHub repo][github_repo].

[boobaa]:https://www.drupal.org/u/boobaa
[czigor]:https://www.drupal.org/u/czigor
[github_repo]:https://github.com/anchal29/comment_alter
[previous_blog]:../../05/30/GSoC-16-Port-Comment-Alter-Module-Week-1.html
