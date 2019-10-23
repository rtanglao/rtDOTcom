---

layout: post
title: "R and Lubridate: How to add week number starting with Firefox release date i.e. Tuesday instead of Sunday or Monday to a dataframe so Tuesday October 22, 2019 - Monday October 28, 2019 is Firefox 70 week 1 and 29Oct-4Nov2019 is FF70 Week 2"
---

# Pontifications

* Very similar to this  previous blog post: [R and Lubridate: How to add daynumber starting with Firefox release date i.e. Tuesday instead of Sunday or Monday to a dataframe](http://rolandtanglao.com/2019/01/08/p1-howto-use-r-lubridate-to-compute-arbitrary-daynumber-for-firefox-release/)
* Again you could  also use lubridate `durations`, but  durations aren’t accurate when you transition  from month to month or year to year so use lubridate `intervals` instead
* Here's the code from   [january-august2019-plot-num-questions-release-weeks-1-4.R](https://github.com/rtanglao/rt-4-week-release-cycle/blob/master/january-august2019-plot-num-questions-release-weeks-1-4.R) : 

```ruby
add_release_week_number <-
  function(df_release,
           yyyy,
           mm,
           dd)
  {
    START_DATE <-
      make_datetime(yyyy, mm, dd, 0, 0, 0,
                    tz = "UTC")
    return (df_release %>%
              mutate(release_week_number =
                       floor(interval(
                         START_DATE, created
                       ) / days(7)) + 1))
  }
```



