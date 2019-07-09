---
layout: post
title: "ggjoy() plot for instagram january 2016 average colour counts"
---

## Pontifications

* Reuse the dataset [https://github.com/rtanglao/2016-r-rtgram/blob/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv](https://github.com/rtanglao/2016-r-rtgram/blob/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv)
* Modify the code in  [https://github.com/rtanglao/2016-r-rtgram/blob/master/twenty-four-square-pie-chart-from-csv.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/twenty-four-square-pie-chart-from-csv.R) to count the colour occurrence by hour (0-23) not the colour occurrences for the whole file
* i.e. in the context of the Nebraska plot the months (January-December) become the colour names (blue-black or whatever it turns out to be) and for the individual "mini-plots", "Mean Temperature F" is the hours 0-23 and the Y Axis is the count for that hour instead of the count of days with that temperature