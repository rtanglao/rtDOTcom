---
layout: post
title: "Simple Density Plot of colournames of Instagram 2017 Average Colour January 2016"
---

## Pontifications

* After [finally understanding density plots](http://rolandtanglao.com/2017/08/18/p1-density-functions-1-variable-and-use-sum-doh/) (thanks Kamyar!), I wrote this code

```R
csv_url = 
"https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"
average_colour_ig_van_jan2016_colourname = read_csv(csv_url)
ggplot(average_colour_ig_van_jan2016_colourname,
aes(colourname)) + geom_density()
```

* And here is the output (I used R Studio to make the output PNG 9740 x 6020 px) on flickr (on github: [pdf](https://github.com/rtanglao/2016-r-rtgram/blob/master/JANUARY2016/naive-density-plot-instagram-vancouver-jan2016-averagecolour-colourname.pdf), [png](https://github.com/rtanglao/2016-r-rtgram/blob/master/JANUARY2016/naive-density-plot-instagram-vancouver-jan2016-averagecolour-colourname.png)):

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36563405901/in/dateposted-ff/" title="naive-density-plot-instagram-vancouver-jan2016-averagecolour-colourname"><img src="https://farm5.staticflickr.com/4377/36563405901_ff4aa4bd3f_n.jpg" width="320" height="198" alt="naive-density-plot-instagram-vancouver-jan2016-averagecolour-colourname"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>