---
layout: post
title: "Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018"
---

## Pontifications

* first populate the database with tags

```bash
./get-sumo-firefox-questions-from-api.rb 2018 09 05 #from current time backwards to september 5, 2018 
./print-csv-tags-unixtime.rb 2018 9 5 2018 9 11 >16september2018-tags-5-11september2018.csv
```

* the resulting CSV file is:
	* [https://github.com/rtanglao/rt-kitsune-api/blob/master/FF62_WEEK1/16september2018-tags-5-11september2018.csv](https://github.com/rtanglao/rt-kitsune-api/blob/master/FF62_WEEK1/16september2018-tags-5-11september2018.csv) 