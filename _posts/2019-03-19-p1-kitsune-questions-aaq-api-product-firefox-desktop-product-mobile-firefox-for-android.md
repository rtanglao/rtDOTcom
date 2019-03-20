---
layout: post
title: "Kitsune Questions aka AAQ API, product == 'firefox' is desktop, 'mobile' is Firefox for android"
---

# Pontifications

* Just to clarify [Kitsune aka support.mozilla.org question API](http://rolandtanglao.com/2018/09/13/kitsune-question-api/)
    * product='```firefox```' is Firefox for desktop e.g. sample API is:
        *  ``` https://support.mozilla.org/api/2/question/?format=json&product=firefox&locale=en-US```
    * product='```mobile```' is Firefox for Android e.g. sample API is:
        * ``` https://support.mozilla.org/api/2/question/?format=json&product=mobile&locale=en-US```