---
layout: post
title: "HowTo: Open support questions tagged escalate" 
---

# Pontifications

* Here's how to open  support questions tagged `escalate` in your browser
*  First, get the questions by updated time i.e. updated may 28, 2020 and then open them in wsl

```bash
../get-by-updated-time-question-url-answers-for-arbitrary-time-period.rb 2020 5 28 2020 5 28 
grep "escalate;" \
updated-2020-05-28-2020-05-28-ff-desktop-creator-answers-desktop-all-locales.csv\
| grep -o '^[0-9]*' |\
xargs -I {} -n 1 wsl-open "https://support.mozilla.org/questions/"{}
```

* where:
  * `xargs -I {`} save the string passed in as `{}`
  * `^[0-9]*'` is a regular expression meaning match numbers at the beginning of the line  until a non number is reached i.e. the `id` field which is an integer and is the first field

* related post from yesterday: [HowTo: Open a random 25% of support questions using shuf and awk and wsl-open](http://rolandtanglao.com/2020/05/27/p1-howto-open-random-25-percent-of-support-questions/)