---
layout: post
title: How to make the simplest possible literal colour as value piechart with a legend
---
# Things to note:

1. If you don't need a legend see [Simplest ggplot2 Pie Chart using colours as literal bar values](http://rolandtanglao.com/2016/07/31/p2-simplest-ggplot2-pie-chart-with-colors-as-bar-values/).
1. Changes from the legend-less version:
    2. in the aes() change TO ```fill=colour``` FROM ```fill=I(colour)```
    3. add ```p = p + scale_fill_manual(values=c("#8B7D7D" = "#8B7D7D", "#4C3F3F" = "#4C3F3F", "#716666" = "#716666"))``` (i'm sure you can automate this colour=colour kludgery that i manully typed!)

## The Code

The code is in [scale-fill-manual-first3-ig-van01january2016-piechart.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/scale-fill-manual-first3-ig-van01january2016-piechart.R). 

```R
library(ggplot2)
data3 = read.csv(
  file="01january2016-1st3datapoints.csv", 
    stringsAsFactors=F)
p = ggplot(data=data3, 
       aes(x=factor(1), fill=colour),)
p= p + geom_bar(stat="count", width=1)
p = p + coord_polar(theta="y", start=0)
p=p+theme_void()
p = p + scale_fill_manual(values=
c("#8B7D7D" = "#8B7D7D", "#4C3F3F" = "#4C3F3F", 
"#716666" = "#716666"))

ggsave("scale-fill-manual-1st3-ig-van-01january-2016-piechart.png", p, width = 26.666666667, height = 26.666666667, dpi = 72, limitsize = FALSE)
```

And here's what [the pie chart with a legend looks like](https://github.com/rtanglao/2016-r-rtgram/blob/master/scale-fill-manual-1st3-ig-van-01january-2016-piechart.png):

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/28611893171/in/dateposted-ff/" title="scale-fill-manual-1st3-ig-van-01january-2016-piechart"><img src="https://c4.staticflickr.com/9/8797/28611893171_a336c6397b.jpg" width="500" height="500" alt="scale-fill-manual-1st3-ig-van-01january-2016-piechart"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
