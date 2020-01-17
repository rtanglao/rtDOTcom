---

layout: post
title: "Week 1 of Firefox 72 Firefox Support Questions: same rolling total as Firefox 70 and 71 so far"
---

# Pontifications

## Code

[https://github.com/rtanglao/rt-kits-api2/blob/master/FF72_ZERO_DAY/cumulative-sum-ffdesktop-ff70-ff72-2019-10-22-2020-01-15-plot-num-questions-release-day-1-28.R](https://github.com/rtanglao/rt-kits-api2/blob/master/FF72_ZERO_DAY/cumulative-sum-ffdesktop-ff70-ff72-2019-10-22-2020-01-15-plot-num-questions-release-day-1-28.R)

```r
library(tidyverse)
library(lubridate)
library(directlabels)
library(RColorBrewer)
add_release_day_number <-
  function(df_release,
           yyyy,
           mm,
           dd)
  {
    START_DATE <-
      make_datetime(yyyy, mm, dd, 0, 0, 0,
                    tz = "UTC")
    
    return (df_release %>%
              mutate(release_day_number =
                       (floor(interval(
                         START_DATE, created
                       ) / days(1))) + 1))
  }

create_desktop_df_release_week_num_questions <-
  function(df, release, yyyy, mm, dd)
  {
    # df is CSV with date time, release is "65"
    # yyyy, mm, dd are integers e.g. 2019, 1, 29
    # remove all questions before january 29, 2019
    ymd_str <- sprintf("%d-%d-%d", yyyy, mm, dd)
    release_start <- ymd(ymd_str, tz = "UTC")
    release_end <- release_start + weeks(4)
    release_questions <-
      df %>% 
      filter(created >= release_start & created < release_end)
    # add day of release week i.e, 1, 2, 3, 4, 5,6, 7..28
    release_questions <-
      add_release_day_number(release_questions, yyyy, mm, dd)
    release_questions <- release_questions %>% 
      group_by(release_day_number) %>% 
      count()
    release_questions <- add_column(release_questions, release = release)
    return (
      release_questions %>% 
      ungroup() %>% 
      dplyr::mutate(cumulutive_sum = cumsum(n)))
  }
oct22_2019_15jan2020_questions <- 
  read_csv("https://raw.githubusercontent.com/rtanglao/rt-kits-api2/master/FF72_ZERO_DAY/sorted-all-desktop-en-us-2019-10-22-2020-01-15-firefox-creator-answers-desktop-all-locales.csv")
# change created unix time to r time UTC using as_datetime()
oct22_2019_5jan2020_questions <- 
  oct22_2019_15jan2020_questions %>%
  mutate(
    created = as_datetime(created, tz = "UTC")
    )


ff70_questions <- create_desktop_df_release_week_num_questions(
  oct22_2019_15jan2020_questions, "70", 2019, 10, 22)
ff71_questions <- create_desktop_df_release_week_num_questions(
  oct22_2019_15jan2020_questions, "71", 2019, 12, 3)
ff72_questions <- create_desktop_df_release_week_num_questions(
  oct22_2019_15jan2020_questions, "72", 2020, 1, 7)
oct22_2019_15jan2020_questions_by_release_week <- 
  bind_rows(ff70_questions, ff71_questions, ff72_questions)

oct22_2019_15jan2020_plot <- 
  ggplot(data=oct22_2019_15jan2020_questions_by_release_week, 
         aes(x=release_day_number, y=cumulutive_sum, group=release, 
             colour = factor(release)))
x_axis = sprintf("%d", seq(1:28))

oct22_2019_15jan2020_plot = oct22_2019_15jan2020_plot +
  geom_line(stat="identity") + 
  labs(color = 'Release Week 1-4') +
  scale_x_discrete(limits = x_axis) +
  coord_cartesian(clip="off") +
  labs(color = 'DesktopAAQ70-72') +
  geom_dl(aes(label = release), method = list(dl.trans(x = x + 0.2), "last.points", cex = 0.8)) +
  geom_dl(aes(label = release), method = list(dl.trans(x = x - 0.2), "first.points", cex = 0.8)) +
  scale_color_brewer(palette = "Dark2")

```

## Output

[https://github.com/rtanglao/rt-kits-api2/blob/master/FF72_ZERO_DAY/plot-cumulative-sum-ffdesktop-ff70-ff72-2019-10-22-2020-01-15-plot-num-questions-release-day-1-28.png](https://github.com/rtanglao/rt-kits-api2/blob/master/FF72_ZERO_DAY/plot-cumulative-sum-ffdesktop-ff70-ff72-2019-10-22-2020-01-15-plot-num-questions-release-day-1-28.png)



<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/49393117746/in/datetaken-public/" title="plot-cumulative-sum-ffdesktop-ff70-ff72-2019-10-22-2020-01-15-plot-num-questions-release-day-1-28"><img src="https://live.staticflickr.com/65535/49393117746_bc100d77c3_w.jpg" width="400" height="261" alt="plot-cumulative-sum-ffdesktop-ff70-ff72-2019-10-22-2020-01-15-plot-num-questions-release-day-1-28"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>