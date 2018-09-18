---
layout: post
title: "Graph of yesterday's Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018"
---

## Pontifications

### code with all the tags with great than 10 occurences

```r
library(ggplot2)
tags = read.csv(file = "https://raw.githubusercontent.com/rtanglao/rt-kitsune-api/master/FF62_WEEK1/16september2018-tags-5-11september2018.csv", stringsAsFactors = F)

p = ggplot(data=tags, aes(x=tag))
p= p + geom_bar(stat="count")
p
library(tidyverse)
tags_with_counts <-
tags %>%
group_by(tag) %>%
count()
tags_count_gt_10 <-
tags_with_counts %>%
filter(n >10)
tags_count_gt_10 <- tags_count_gt_10 %>% arrange(n)
p2 = ggplot(data=tags_count_gt_10, aes(x=tag, y=n))
p2 = p2 + geom_bar(stat="identity")
p2 = p2 + theme(axis.text.x = element_text(angle = 90, hjust = 1))
p2
```

### graph with all the tags with greater than 10 occurences

* The graph from yesterday's [Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018](http://rolandtanglao.com/2018/09/16/p1-firefox62-sumo-support-forum-tags-week1/):

![All tags for the first week of Firefox Desktop 62 i.e. September 5-11, 2018](https://github.com/rtanglao/rt-kitsune-api/raw/master/FF62_WEEK1/sumo-firefox-desktop-62-week1-05-11september2018-all-tags-count-gt-10-Rplot02.png)