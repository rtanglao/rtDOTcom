---
layout: post
title: "Jan 1, 2019 - April 18, 2019 - 22 (out of 5539 i.e. 0.4%) SUMO Firefox desktop Forum questions about losing two factor authentication codes"
---

# Pontifications

* over 3.5 months 0.4 % of SUMO Firefox desktop questions were about losing 2FA codes (22 out of 5539)

## Colophon

```bash
./print-2fa-sumo-questions.rb 2019 1 1 2019 4 18 2>01jan2019-18january-2fa-stderr-out.txt\
>01january2019-18january2019-2fa-sumo-forum-question-ids.txt
cat 01january2019-18january2019-2fa-sumo-forum-question-ids.txt | ./open-ids-in-browser.rb
# which leads to 33 questions, some of which are off topic and duplicates
```
* manually remove duplicates and off topic and you end up with 22 questions in 4.5 months:
[offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.txt](https://github.com/rtanglao/rt-kitsune-api/blob/master/offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.txt)
