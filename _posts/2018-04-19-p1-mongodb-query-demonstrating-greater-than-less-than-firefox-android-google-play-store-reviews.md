---
layout: post
title: "MongoDB queries showing less than, greater than resulting in: Number of English only, 1 and 2 star: Non replied to Firefox for Android reviews November 14, 2017 - April 18, 2018 is: 3962"
---

## Pontifications

* Used the following mongodb query from [https://github.com/rtanglao/rt-fennec-gplay](https://github.com/rtanglao/rt-fennec-gplay) which returns 3962 documents:

```js

{"synthetic_developer_should_have_replied_but_did_not_reply" : true, 
  "Review Last Update Date and Time": 
    {$gte : "2017-11-14 00:00:00 UTC"},
  "star_rating": { $lt : 3},
  "Reviewer Language": "en"
}
```



