---
layout: post
title: "R and Lubridate: How to add daynumber starting with Firefox release date i.e. Tuesday instead of Sunday or Monday to a dataframe"
---
# Pontifications

* Following up from yesterday's [R and Lubridate: Calculating Time Differences in R using intervals aka a better way to compute daynumber starting from arbitrary day of the week](title: "R and Lubridate: How to add daynumber starting with Firefox release date i.e. Tuesday to a dataframe")

```r
add_release_day_number <- function(
  df_release,
  yyyy,
  mm,
  dd
) 
{  
  START_DATE <- 
  make_datetime(
    yyyy, mm, dd, 0,0,0, 
    tz = "America/Vancouver"
    )
  
  return (
    df_release %>% 
      mutate(
        release_week_day_number = 
        floor(
            interval(START_DATE, created) / days(1)
            ) + 1
        )
  )
}
```

* The above ^^^^ is the most accurate and the best way to compute [daynumber starting at an arbitrary day of the week e.g. Tuesday for Firefox releases](http://rolandtanglao.com/2019/01/06/p1-lubridate-ydate-to-release-week-daynumber/)! 
You can also use lubridate ```durations```, but 
durations aren't accurate when you transition 
from month to month or year to year