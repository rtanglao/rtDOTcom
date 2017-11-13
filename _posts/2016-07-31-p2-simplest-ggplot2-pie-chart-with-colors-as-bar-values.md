---
layout: post
title: Simplest ggplot2 Pie Chart using colours as literal bar values
---
# Things to note:

1. There is a 1 line change to [the previous blog post about the simplest possible bar chart](http://rolandtanglao.com/2016/07/31/p1-simplest-ggplot2-bar-chart-with-colors-as-bar-values/) to make the bar cart a pie chart. Just add: ```p = p + coord_polar(theta="y", start=0)```.
2. This results in a legend-less pie chart. See [How to make the simplest possible literal colour as value piechart with a legend](http://rolandtanglao.com/2016/07/31/p3-simplest-ggplot2-pie-chart-with-colors-as-bar-values-and-a-legend/).


And here's what [the pie chart  looks like](https://github.com/rtanglao/2016-r-rtgram/blob/master/1st3-ig-van-01january-2016-piechart.png):

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/28657101336/in/dateposted-ff/" title="1st3-ig-van-01january-2016-piechart"><img src="https://c1.staticflickr.com/9/8447/28657101336_828f1fef0a.jpg" width="500" height="500" alt="1st3-ig-van-01january-2016-piechart"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
