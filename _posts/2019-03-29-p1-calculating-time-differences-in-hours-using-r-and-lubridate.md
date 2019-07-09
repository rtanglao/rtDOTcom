---
layout: post
title: "07January2019 how to calculate time differences for support using R and lubridate"
---

# Pontifications

*  forgot to blog this: [07January2019 how to calculate time differences in hours for support using R and lubridate](https://github.com/rtanglao/rt-making-r-and-rstudio-work-for-me#07january2019-how-to-calculate-time-differences-for-support)

```r
interval(ymd_hms("2019-01-04 18:40:00", 
  tz = "America/Vancouver"), 
  ymd_hms("2019-01-07 12:59:00", 
    tz = "America/Vancouver")) / hours(1)
[1] 66.31667
```

