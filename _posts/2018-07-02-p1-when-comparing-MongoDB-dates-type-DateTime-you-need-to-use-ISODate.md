---
layout: post
title: "MongoDB: When comparing dates of type DateTime you need to convert strings to ISODate"
---

## Pontifications
* **i.e. the following MongoDB query doesn't work:**

```js
{"Developer Reply Text": {$ne: null}, 'developer_last_updated_time': 
  {$gte:  "2018-05-16T00:00:00Z"}}
```

* but the following does work

```js
{"Developer Reply Text": {$ne: null}, 'developer_last_updated_time': {$gte: { $date: "2018-05-16T00:00:00Z"} }}
```

* this also works and is the form I prefer since it seems less complicated to me:

```js
{"Developer Reply Text": {$ne: null}, 'developer_last_updated_time': {
  '$gte': ISODate("2018-05-16T00:00:00Z") }}
```

