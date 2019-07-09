---
layout: post
title: "R and Lubridate: How do I get daynumber starting at arbitrary day of the week? e.g. Firefox day 1 of a release week usually starts on Tuesday"
---
# Pontifications

* Using R and lubridate, I don't know how to reset the start of the year to be an arbitrary day of the year i.e. the day Firefox is released which is usually a Tuesday and sometimes Wednesday.
* It would be cool if there was something analogous to ```lubridate.week.start``` e.g. something like ```lubridate.year.start```
* For now I kludged (this doesn't work if the first 3 weeks of the release spans years e.g. dec 2018-2019 or if there is a leap year) it in [plot-antivirus-mentions-by-week.R](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/plot-antivirus-mentions-by-week.r) by subtracting the day of the year and adding 1:
* e.g. in the following code, if Firefox 62 was released on September 5, 2018 which is yday 248 let's call it ```release_yday```, then the days since September 5th is ```yday - release_yday + 1```

```r
base_yday = yday(one_day_of_data_from_mongo[1,"created"]) 

...

 mutate(release_week_day_number = yday(created) - base_yday + 1)
```