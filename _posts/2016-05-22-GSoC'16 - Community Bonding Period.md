---
layout: post
title: GSoC'16 - Community bonding period
categories:
- blog
---

---

> Google Summer of Code (GSoC) is a global program that matches students up with open source, free software and technology-related organizations to write code and get paid to do it! The organizations provide mentors who act as guides through the entire process, from learning about the community to contributing code. The idea is to get students involved in and familiar with the open source community and help them to put their summer break to good use. For any information related to GSoC I would recommend to visit the [manual page](https://developers.google.com/open-source/gsoc/resources/manual#student_manual).

The results of GSoC'16 came out on 23rd of April and and I was happy to find out that I was selected. I would like to thank my mentors - László Csécsy([boobaa](https://www.drupal.org/u/boobaa)) and Czövek András([czigor](https://www.drupal.org/u/czigor)), [slurpee](https://www.drupal.org/u/slurpee) and [cs_shadow](https://www.drupal.org/u/cs_shadow) for providing necessary suggestions while preparing my proposal. Getting accepted for the Google Summer of Code marked the beginning of the Community bonding period. The community bonding period is all about, well, community bonding. Rather than jumping straight into coding, you've got some time to learn about your organization's processes - release and otherwise - developer interactions, codes of conduct, etc.

**Project:** Porting Comment Alter module to Drupal 8.

**Community Bonding Period**
I had my semester exams, projects and assignments so I couldn't give it a lot of time but I remained in contact with my mentors ([boobaa](https://www.drupal.org/u/boobaa) and [czigor](https://www.drupal.org/u/czigor)). We were in constant touch via mail and also we [had](https://github.com/anchal29/comment_alter) a hangout meeting last Friday over which we had the following discussion:

* I'll be maintaining my code initially on github. The repo can be accessed [here](https://github.com/anchal29/comment_alter).
* My mentors will be reviewing my code on daily basis during most of the working days and I'll proceed function by function of the D7 module for the port as it was explained in the proposal in detail.

I went through some of the references as I mentioned in my proposal. These references covered Form API, Configuration API and Comment module in which I tried to cover the following things:

* Form API: I created some small modules by using the Form API and also I tried to go through altering the forms using hooks which are to be used in the module.
* Configuration API: In configurational API I went through the configuration schema part of it which will be used in the module for form_alter using third party settings.
* menu_ui is one of the good examples which I found in core which implements hook_form_BASE_FORM_ID_alter by using third party settings.

I'm thankful to László Csécsy for providing me with exercises for the past couple of months which helped me getting a better understanding of Drupal and the module. I have created
some modules which covered the basics of Form API. We used Acquia Cloud as our hosting solution where our work can be seen ([Link to the page](http://anchal298pygasvddu.devcloud.acquia-sites.com/)). I also went through a few issues related to the module and provided patch for it.
Since the coding period has started now, the next blog will be on my progress over the first week of coding.
