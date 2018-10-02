---
layout: post
title: "R Package directlabels allows you to label end of lines, group_by() allows you to group by multiple variables; krazy idea: watch for spikes in FF questions by operating system"
---

## Pontifications

* one krazy idea would be to plot number of support questions by hour and day by operating system and send an alert if they vary say by more than plus/minus 20% than the previous day<--- i did this on a daily basis for Thunderbird back in 2010 for email providers
* Don't know how I ended up at [Plot labels from ends of lines on stackoverflow](https://stackoverflow.com/questions/29357612/plot-labels-at-ends-of-lines)  but from it I learned that the R package [directlabels](http://directlabels.r-forge.r-project.org/)  allows you label end of lines in ggplot2
* And ```group_by()``` allows you to group by multiple variables e.g. ```group_by(os, week)``` allows you to group by operating system and week which is how you plot by OS and week
* This allows me to make [last week's FF62 operating system plot](http://rolandtanglao.com/2018/09/27/p1-firefox62-operating-system-line-graph-sumo-support-questions-first-3-weeks/) more legible by labelling the OS lines individually.

### Code
  * From https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/01october2018-ff62-operating-system-directlabels.r
  
```r
library(tidyverse)
library(directlabels)
# I found direct labels from this stack overflow thread:
# https://stackoverflow.com/questions/29357612/plot-labels-at-ends-of-lines
# output:
# https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/01october2018-ff62-operating-system-directlabels-Rplot13.png
week1_to_week3_os_tags <-
  read_csv(
    "https://raw.githubusercontent.com/rtanglao/rt-kitsune-api/master/FF62_WEEK1_TO_3/26september2018-week1-week3-weeknumber-tags.csv") %>% 
  filter(
    grepl("^windows-", tag) |
    grepl("^mac-os", tag) |
    (tag == "linux")) %>%
  mutate(os=ifelse(grepl("^windows-", tag), "windows", tag)) %>% 
  mutate(os=ifelse(grepl("^mac-os", tag), "mac-os", tag)) %>% 
  filter(tag != "windows-active-directory") %>% 
  group_by(os, week) %>%
  count()
label_at_end_week1_to_week3_os_line_plot <-
  ggplot(data=week1_to_week3_os_tags, aes(
    x=week, y=n, group= os, colour = os))
label_at_end_week1_to_week3_os_line_plot = label_at_end_week1_to_week3_os_line_plot + 
  geom_line(stat="identity") + 
  labs(color = 'Firefox 62 Desktop OS 5-25Sep2018') +
  scale_x_discrete(limits = c("1", "2", "3")) +
  geom_dl(aes(label = os), method = list(dl.trans(x = x + 0.2), "last.points", cex = 0.8)) +
  geom_dl(aes(label = os), method = list(dl.trans(x = x - 0.2), "first.points", cex = 0.8))
```

### Output

![01october2018-ff62-operating-system-directlabels-Rplot13.png](https://github.com/rtanglao/rt-kitsune-api/raw/master/VISUALIZATIONS/01october2018-ff62-operating-system-directlabels-Rplot13.png)


