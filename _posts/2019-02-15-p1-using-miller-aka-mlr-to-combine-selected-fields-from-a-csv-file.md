---
layout: post
title: "Using mlr aka miller to combine selected fields from multiple CSV files"
---
# Pontifications

* I think it's worth pulling out the [miller aka mlr](https://github.com/johnkerl/miller) bits from [Users don't know when their antivirus breaks Firefox and it's not obvious to them so they don't mention it in their support requests](http://rolandtanglao.com/2019/02/10/p1-users-dont-know-antivirus-is-breaking-firefox-and-it-not-obvious-when-it-does/) because combining selected fields CSV files is a common thing to do:

```bash
mlr --csv cut -x -f  'product,topic,tags'  firefox*.csv > ff58-65-id-created-title-content-firefoxversion-1streleaseweek-day.csv
```

where:

  * ```product, topic, tags``` are the fields to cut out
  * ```firefox*.csv``` are the CSV files to combine