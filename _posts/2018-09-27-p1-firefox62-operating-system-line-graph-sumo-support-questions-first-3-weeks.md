---
layout: post
title: "R ggplot2 line graph of the first 3 weeks of Firefox 62 desktop SUMO support questions operating systems"
---

## Pontifications

* Compare and contrast with [yesterday's bar graph of the same data](http://rolandtanglao.com/2018/09/26/p1-firefox62-operating-system-graph-sumo-support-questions-first-3-weeks/)! 
* [Here's the R code](https://github.com/rtanglao/rt-kitsune-api/blob/master/FF62_WEEK1_TO_3/ff62-desktop-operating-system-first-3-weeks.r):

```r
# the following code was run in R Studio
# output: 
# https://github.com/rtanglao/rt-kitsune-api/raw/master/FF62_WEEK1_TO_3/Firefox%2062%20Desktop%20Operating%20System%20SUMO%20Questions%205-25%20September2018.png
library(tidyverse)
week1_to_week3_os_tags <-
  read_csv(
    "https://raw.githubusercontent.com/rtanglao/rt-kitsune-api/master/FF62_WEEK1_TO_3/26september2018-week1-week3-weeknumber-tags.csv") %>% 
  filter(
    grepl("^windows-", tag) |
    grepl("^mac-os", tag) |
    (tag == "linux")) %>%
  mutate(os=ifelse(grepl("^windows-", tag), "windows", tag)) %>% 
  mutate(os=ifelse(grepl("^mac-os", tag), "mac-os", tag)) %>% 
  filter(tag != "windows-active-directory")
week1_to_week3_os_plot <-
  ggplot(data=week1_to_week3_os_tags, aes(x=week, fill=os))
week1_to_week3_os_plot = week1_to_week3_os_plot + 
  geom_bar(stat="bin", bins = 3,
  position="dodge")
week1_to_week3_os_line_plot <-
  ggplot(data=week1_to_week3_os_tags, aes(
    x=week, fill=os, colour = os))
week1_to_week3_os_line_plot = week1_to_week3_os_line_plot + 
  geom_line(stat="bin", bins = 3) + 
  scale_color_manual(values = c(
    'windows-10' = 'green',
    'linux' = 'purple',
    'mac-os' = 'orange',
    'windows-7' = 'pink',
    'windows-8' = 'blue',
    'windows-81' = 'brown',
    'windows-server-2016' = 'magenta',
    'windows-vista' = 'black',
    'windows-xp' = 'dark green')) +
  labs(color = 'FF62 OS 5-25Sep2018')
```
* Here's the output:

	<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/30018293677/in/dateposted-public/" title="Firefox 62 Desktop Operating System SUMO Questions 5-25 September2018"><img src="https://farm2.staticflickr.com/1964/30018293677_eddcb2aab6_n.jpg" width="199" height="320" alt="Firefox 62 Desktop Operating System SUMO Questions 5-25 September2018"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>