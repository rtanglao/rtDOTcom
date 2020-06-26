---
layout: post
title: "How To get a list of escalated Firefox Desktop Support Questions"
---
* From the [rt-kits-api2 README](https://github.com/rtanglao/rt-kits-api2#25june2020-add-titles-to-email-escalation-report):

```bash
cd 202006
../get-by-updated-time-question-url-answers-for-arbitrary-time-period.rb \
2020 6 22 2020 6 25
cd ..
grep "escalate;" \
202006/updated-2020-06-22-2020-06-25-ff-desktop-creator-answers-desktop-all-locales.csv\
| ./with-title-email-escalations.rb
```

