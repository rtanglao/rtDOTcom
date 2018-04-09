---
layout: post
title: "Mongodb query in javascript showing '$or' syntax"
---

## Pontifications
 
```js
{  
  "firefox_major_version" : 57,  
  "Reviewer Language" : "en",  
  "$or" : [{"star_rating" : 1 }, {"star_rating" : 2}]
}
```