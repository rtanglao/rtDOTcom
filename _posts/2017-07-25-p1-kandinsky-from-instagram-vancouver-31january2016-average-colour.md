---
layout: post
title: "Turn Vancouver Instagram 31January2016 average colour dataset into a Kandinsky-like image using R"
---

## Pontifications

* Using the [wonderful Kandinsky R package](http://giorasimchoni.com/2017/07/30/2017-07-30-data-paintings-the-kandinsky-package/)
* Here's a sample "Kandinsky-like" image from [average colour instagram vancouver 31 january 2016](https://github.com/rtanglao/2016-r-rtgram/blob/master/JANUARY2016/31-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv)!
<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/35335109114/" title="kandinsky-31jan2016-vancouver-instagram"><img src="https://farm5.staticflickr.com/4316/35335109114_516693702f.jpg" width="500" height="272" alt="kandinsky-31jan2016-vancouver-instagram"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

### COLOPHON

```R
library(kandinsky)
data3 = read.csv(file = \
"~rtanglao/Dropbox/GIT/2016-r-rtgram/JANUARY2016/31-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv", \
stringsAsFactors = F)
kandinsky(data3$colour)
```