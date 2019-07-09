---
layout: post
title: "Part 3 - mpg scatterplot - applied to average colour instagram by hour jan 1-31, 2016 - create naive colourname visualization with black dots"
---

## Pontifications

* [Part 1](http://rolandtanglao.com/2017/08/07/p1-mpg-scatterplot-average-colour-instagram-r-data-science/), [Part 2](http://rolandtanglao.com/2017/08/07/p2-part2-create-csv-files-with-plotrix-colour-names/)
* First, here's the output. The difference from part 1 is that the roughly 600 colournames from the ```plotrix``` R package are used so there are 600 values on the y axis not 100K:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36040620820/in/dateposted-ff/" title="part3-naive-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname"><img src="https://farm5.staticflickr.com/4334/36040620820_e30ca68eb5_n.jpg" width="320" height="174" alt="part3-naive-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* Here's the relevant code from [https://github.com/rtanglao/2016-r-rtgram/blob/master/part3-create-naive-scatterplot-colourname-hour.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/part3-create-naive-scatterplot-colourname-hour.R) : 

```R
csv_url = "https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"
average_colour_ig_van_jan2016_colourname = read_csv(csv_url)
plot =
    ggplot(data=average_colour_ig_van_jan2016_colourname)+
    geom_point(mapping = aes(x = hour, y=colourname))
filename = "part3-naive-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.png"
  ggsave(filename,
         plot,
         width = 53.333333333,
         height = 29.069444444,
         dpi = 72,
         limitsize = FALSE,
         bg = "transparent"
         )
```

* All the dots are black since there is no colour aesthetic.
* This RScript was invoked as follows:

```bash
cd JANUARY2016
Rscript ../part3-create-naive-scatterplot-colourname-hour.R
```

* In [Part 4](http://rolandtanglao.com/2017/08/07/p4-part4-ig-van-jan2016-colour-the-dots-with-the-right-colour-name/), we'll create a visualization with the dots coloured according to the colour names.