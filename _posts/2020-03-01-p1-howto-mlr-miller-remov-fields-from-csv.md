---
layout: post
title: "How to: retain selected fields and remove the rest in a CSV file using mlr aka miller"
---

# Pontifications

* The following miller aka `mlr` script removes all fields except `title`and `content`
````bash
mlr --csv cut -f title,content id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv 
````

* (previously blogged not as clearly: [Using mlr aka miller to combine selected fields from multiple CSV files](http://rolandtanglao.com/2019/02/15/p1-using-miller-aka-mlr-to-combine-selected-fields-from-a-csv-file/))

