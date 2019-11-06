---

layout: post
title: "Firefox 70 Desktop looks to be a quiet release compared to FF65-69 based on the cumulative sum of the SUMO Forum questions in the first two weeks"
---

# Pontifications

* Based on the plot below, showing the first two weeks of Firefox 70 Desktop, it looks like Firefox 70 in the first four weeks will be a quiet release. (see earlier post: [Firefox 65-69 Cumulative Sum Day 1-28 of Firefox Support Questions on support.mozilla.org](http://rolandtanglao.com/2019/11/02/p1-firefox-65-69-cumulative-sum-sumo-support-forum-questions/))
* I could be wrong of course :-) and something could emerge in the next two weeks.

## Plot: Firefox 70 first two weeks and Firefox 65-69 first four weeks: cumulative sum  of SUMO Forum desktop questions

<a data-flickr-embed="true" data-header="true" data-footer="true" href="https://www.flickr.com/photos/roland/49017411486/in/photolist-2hFv3Gf-2hEaCtg-2hxMftz-2hxQYub-2hxQ2vc-2hxkkxC-24QVji4-2emwTeu-2emcywY-2e4fbiX-RDTSr2-Tgff6h-Tgf6d7-2dAmZ49-So3kZ1-2d6imeP-2d4wp92-TsWUFs-2fwzxrN-TiT42s-2e4ctF8-2fouZmk-2fouYwp-2dkqcvh-2djoCEf-2cnYPtw-2aGLJ3y-PfSm4z-2a6LJ4q-2cSgTfz-2cSagmT-2a6CL4U-2aWS6ke-2aWRWCp-2cgvqhZ-2aSEDfp-2a4WHbv-2doRZvy-2bhK9eo-29ANbMC-Pu5EmA-28NktfY-2asK9Em-Pqocw1-Pq873q-MJBATx-28Hkxej-2a4WHde-2a4WH7T-26FmE3B" title="720bc46-cumulative-sum-unfaceted-january-04november2019-plot-num-questions-release-day-1-28"><img src="https://live.staticflickr.com/65535/49017411486_72cc5cfb13.jpg" width="500" height="361" alt="720bc46-cumulative-sum-unfaceted-january-04november2019-plot-num-questions-release-day-1-28"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## Code for the above plot

[cumulative-sum-unfaceted-january-04november2019-plot-num-questions-release-day-1-28.R](https://github.com/rtanglao/rt-4-week-release-cycle/blob/master/cumulative-sum-unfaceted-january-04november2019-plot-num-questions-release-day-1-28.R) : 

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
jan_04nov_2019_questions <- 
  read_csv("https://raw.githubusercontent.com/rtanglao/rt-kits-api2/master/2019BYMONTH/concatenated-2019-01-01-2019-11-04-firefox-creator-answers-desktop-all-locales.csv")
# change created unix time to r time UTC using as_datetime()
jan_04nov_2019_questions <- 
  jan_04nov_2019_questions %>%
  mutate(
    created = as_datetime(created, tz = "UTC")
    )

ff65_questions <- create_desktop_df_release_week_num_questions(
  jan_04nov_2019_questions, "65", 2019, 1, 29)
ff66_questions <- create_desktop_df_release_week_num_questions(
  jan_04nov_2019_questions, "66", 2019, 3, 19)
ff67_questions <- create_desktop_df_release_week_num_questions(
  jan_04nov_2019_questions, "67", 2019, 5, 21)
ff68_questions <- create_desktop_df_release_week_num_questions(
  jan_04nov_2019_questions, "68", 2019, 7, 9)
ff69_questions <- create_desktop_df_release_week_num_questions(
  jan_04nov_2019_questions, "69", 2019, 9, 3)
ff70_questions <- create_desktop_df_release_week_num_questions(
  jan_04nov_2019_questions, "70", 2019, 10, 22)
jan_04nov_2019_questions_by_release_week <- 
  bind_rows(ff65_questions, ff66_questions, ff67_questions, 
            ff68_questions, ff69_questions, ff70_questions)

jan_04nov_2019_plot <- 
  ggplot(data=jan_04nov_2019_questions_by_release_week, 
         aes(x=release_day_number, y=cumulutive_sum, group=release, 
             colour = factor(release)))
x_axis = sprintf("%d", seq(1:28))

jan_04nov_2019_plot = jan_04nov_2019_plot +
  geom_line(stat="identity") + 
  labs(color = 'Release Week 1-4') +
  scale_x_discrete(limits = x_axis) +
  coord_cartesian(clip="off") +
  labs(color = 'DesktopAAQ65-70') +
  geom_dl(aes(label = release), method = list(dl.trans(x = x + 0.2), "last.points", cex = 0.8)) +
  geom_dl(aes(label = release), method = list(dl.trans(x = x - 0.2), "first.points", cex = 0.8)) +
  scale_color_brewer(palette = "Dark2")
```