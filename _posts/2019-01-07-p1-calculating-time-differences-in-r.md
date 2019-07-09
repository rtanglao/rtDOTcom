---
layout: post
title: "R and Lubridate: Calculating Time Differences in R using intervals aka a better way to compute daynumber starting from arbitrary day of the week"
---
# Pontifications

* the following is from [my new repo about r and r studio tips and tricks](https://github.com/rtanglao/rt-making-r-and-rstudio-work-for-me#07-january-2019-how-to-calculate-time-differences-for-support)

```r
interval(ymd_hms("2019-01-04 18:40:00", 
  tz = "America/Vancouver"), 
  ymd_hms("2019-01-07 12:59:00", 
    tz = "America/Vancouver")) / hours(1)
[1] 66.31667
```

* The above ^^^^ is the most accurate and the best way to compute [daynumber starting at an arbitrary day of the week e.g. Tuesday for Firefox releases](http://rolandtanglao.com/2019/01/06/p1-lubridate-ydate-to-release-week-daynumber/)! 
You can also use lubridate ```durations```, but 
durations aren't accurate when you transition 
from month to month or year to year