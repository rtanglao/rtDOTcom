---

layout: post
title: "Firefox 65-68: Number of desktop questions on support.mozilla.org by release week for the first 4 weeks of a release"
---

# Pontifications

* Reacquainted myself with the wonders :-)  of  `ggplot2` faceted plots and the awesomeness of `lubridate`.

## Code: january-august2019-plot-num-questions-release-weeks-1-4.R

[january-august2019-plot-num-questions-release-weeks-1-4.R](https://github.com/rtanglao/rt-4-week-release-cycle/blob/master/january-august2019-plot-num-questions-release-weeks-1-4.R) :

```r
library(tidyverse)
library(lubridate)
library(directlabels)
library(RColorBrewer)
add_release_week_day_number <-
  function(df_release,
           yyyy,
           mm,
           dd)
  {
    START_DATE <-
      make_datetime(yyyy, mm, dd, 0, 0, 0,
                    tz = "UTC")
    
    return (df_release %>%
              mutate(release_week_day_number =
                       ((floor(interval(
                         START_DATE, created
                       ) / days(1))) %% 7) + 1))
  }
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
    # add release week number i.e. 1, 2,3, or 4
    release_questions <- 
      add_release_week_number(release_questions, yyyy,mm, dd) 
    # add day of release week i.e, 1, 2, 3, 4, 5,6, 7
    release_questions <-
      add_release_week_day_number(release_questions, yyyy, mm, dd)
    release_questions <- release_questions %>% 
      group_by(release_week_number, release_week_day_number) %>% 
      count()
    
    add_column(release_questions, release = release)
  }
jan_aug_2019_questions <- read_csv("https://raw.githubusercontent.com/rtanglao/rt-kitsune-api/master/01jan2019-31aug2019.csv")
# change created unix time to r time UTC using as_datetime()
jan_aug_2019_questions <- 
  jan_aug_2019_questions %>%
  mutate(
    created = as_datetime(created, tz = "UTC")
    )

ff65_questions <- create_desktop_df_release_week_num_questions(
  jan_aug_2019_questions, "65", 2019, 1, 29)
ff66_questions <- create_desktop_df_release_week_num_questions(
  jan_aug_2019_questions, "66", 2019, 3, 19)
ff67_questions <- create_desktop_df_release_week_num_questions(
  jan_aug_2019_questions, "67", 2019, 5, 21)
ff68_questions <- create_desktop_df_release_week_num_questions(
  jan_aug_2019_questions, "68", 2019, 7, 9)
jan_aug_2019_questions_by_release_week <- 
  bind_rows(ff65_questions, ff66_questions, ff67_questions, ff68_questions)

jan_aug_2019_plot <- 
  ggplot(data=jan_aug_2019_questions_by_release_week, 
         aes(x=release_week_day_number, y=n, group=release_week_number, 
             colour = factor(release_week_number)))
jan_aug_2019_plot = jan_aug_2019_plot +
  geom_line(stat="identity") + 
  labs(color = 'Release Week 1-4') +
  scale_x_discrete(limits = c("1", "2", "3", "4", "5", "6","7")) +
  labs(color = 'DesktopAAQ65-68') +
  geom_dl(aes(label = release_week_number), method = list(dl.trans(x = x + 0.2), "last.points", cex = 0.8)) +
  geom_dl(aes(label = release_week_number), method = list(dl.trans(x = x - 0.2), "first.points", cex = 0.8)) +
  scale_color_brewer(palette = "Dark2")+
  facet_wrap(~release)

```

## Plot

<a data-flickr-embed="true" data-header="true" data-footer="true" href="https://www.flickr.com/photos/roland/48924985086/in/datetaken/" title="34fcc3d-DesktopAAQ65-68Week1-4"><img src="https://live.staticflickr.com/65535/48924985086_43a7397786.jpg" width="500" height="339" alt="34fcc3d-DesktopAAQ65-68Week1-4"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>



