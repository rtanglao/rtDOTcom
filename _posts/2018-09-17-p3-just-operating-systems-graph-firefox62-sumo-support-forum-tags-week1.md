---
layout: post
title: "Just Operating System bar graph of yesterday's Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018"
---

## Pontifications

* see [previous post](http://rolandtanglao.com/2018/09/17/p1-the-graph-firefox62-sumo-support-forum-tags-week1/) for the code that this builds on 

### code with  just the operating system tags

* ```read_csv``` is better because it doesn't require any arguments and it's faster
* code from [Tim Smith](https://github.com/tdsmith), thanks Tim!

```r
os_tags <-
read_csv("https://raw.githubusercontent.com/rtanglao/rt-kitsune-api/master/FF62_WEEK1/16september2018-tags-5-11september2018.csv") %>%
filter(
grepl("^windows-", tag) |
(tag == "mac-os") |
(tag == "linux")) %>%
mutate(os=ifelse(grepl("^windows-", tag), "windows", tag))
os_tags_with_counts <-
  os_tags %>%
  group_by(os) %>%
  count()
os_plot <-
  ggplot(data=os_tags_with_counts, aes(x=os,y=n))
os_plot = os_plot + geom_bar(stat="identity")
```

### graph with just operating systems

* The graph from yesterday's [Firefox 62 Desktop SUMO Support Forums Week 1 tags - September 5-11, 2018](http://rolandtanglao.com/2018/09/16/p1-firefox62-sumo-support-forum-tags-week1/):
* **clearly shows that Windows is the operating system for the vast majority of user support questions (at least on SUMO but probably elsewhere)**

![Just Operating system tags (linux, mac, windows)  for the first week of Firefox Desktop 62 i.e. September 5-11, 2018](https://github.com/rtanglao/rt-kitsune-api/raw/master/FF62_WEEK1/osplot-week1-ff62-desktop.md.png)