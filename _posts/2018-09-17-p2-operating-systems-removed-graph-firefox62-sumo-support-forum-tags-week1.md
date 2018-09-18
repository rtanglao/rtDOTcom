---
layout: post
title: "Operating System removed Graph of yesterday's Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018"
---

## Pontifications

* see [previous post](http://rolandtanglao.com/2018/09/17/p1-the-graph-firefox62-sumo-support-forum-tags-week1/) for the code that this builds on 

### code with all the operating system tags removed 

```r
tags_gt10_remove_common_tags <-
tags_count_gt_10 %>%
  filter(tag != "desktop" &
    tag != "escalate" &
    tag != "beta" &
    tag != "esr" &
    tag != "firefox-520" &
    tag != "firefox-600" &
    tag != "firefox-610" &
    tag != "firefox-6102" &
    tag != "firefox-620" &
    tag != "firefox-630" &
    tag != "linux" &
    tag != "mac-os" &
    tag != "needsinfo" &
    tag != "other" &
    tag != "rolandff62experiment" &
    tag != "windows-10" &
    tag != "windows-7" &
    tag != "windows-81" &
    tag != "windows-xp" )
p3 = ggplot(data=tags_gt10_remove_common_tags, aes(x=tag, y=n))
p3 = p3 + geom_bar(stat = "identity")
p3 = p3 + theme(axis.text.x = element_text(angle = 90, hjust = 1))
p3
```

### graph with all the operating system tags removed

* The graph from yesterday's [Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018](http://rolandtanglao.com/2018/09/16/p1-firefox62-sumo-support-forum-tags-week1/):

![Operating system tags (linux, mac, windows) removed for the first week of Firefox Desktop 62 i.e. September 5-11, 2018](https://github.com/rtanglao/rt-kitsune-api/raw/master/FF62_WEEK1/linux-removed-Operating%20System%20tags%20removed%20for%20the%20first%20week%20of%20Firefox%20Desktop%2062%20i.e.%20September%205-11Rplot02.png)