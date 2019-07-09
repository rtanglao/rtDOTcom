---
layout: post
title: "21000 px wide, theme_void(), Simple Density Plot of colournames of Instagram 2017 Average Colour January 2016"
---

## Pontifications

* To the [previous naive density plot](http://rolandtanglao.com/2017/08/20/p1-naive-density-plot-instagram-vancouver-average-colour-january-2016/), I changed to ```theme_void()``` and made it 21000 pixel wide: [plot on github](https://github.com/rtanglao/2016-r-rtgram/commit/3aab373eb4d8c46f2a420014ca9687d717f39921)
* Still have issues with 1.0 spikes which shouldn't happen, everything should be less than 1.0! I will investigate, error in the dataset? (I noticed that azure might be problematic?)
* Here is the R code that I ran in R Studio

```R
csv_url = 
"https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"
average_colour_ig_van_jan2016_colourname = 
  read_csv(csv_url)
ggplot(average_colour_ig_van_jan2016_colourname,
 aes(colourname)) + geom_density() + theme_void()

```