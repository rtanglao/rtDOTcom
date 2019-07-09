---
layout: post
title: Simplest possible R square pie chart aka waffle chart
---

Sometime after 1000 squares this fails, I do not yet know why :-) !

## Code

[first6-ig-van-01january2016-square-piechart.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/first6-ig-van-01january2016-square-piechart.R)

```R
library(ggplot2)
library(waffle)
library(plotrix)
library(plyr)

tc <-
     function(x) {
         return (head(color.id(x),n=1))
     }

data6 = read.csv(
  file="6datapoints-01jan2016.csv",
    stringsAsFactors=F)

data6$colourname <- sapply(data6$colour, tc)

countcolourname = count(data6, "colourname")
countcolourname <- countcolourname[order(-countcolourname$freq),]

colour_vector <-setNames(countcolourname$freq, countcolourname$colourname)
p = waffle(colour_vector, rows=1, size=0.5, 
    colors=I(data6$colour))

ggsave("6datapoints-squarepiechart.png", p, width = 26.666666667, height = 26.666666667, dpi = 72, limitsize = FALSE) # 26.6666667 = 1920/72dpi
warnings()
```

## Dataset
[6datapoints-01jan2016.csv](https://github.com/rtanglao/2016-r-rtgram/blob/master/6datapoints-01jan2016.csv)

```csv
colour,id,dayofweek-month-dayofmonth,daynumber
#8B7D7D,1152722080165873450_545005592,FriJan1,1
#4C3F3F,1152722094194289757_285178194,FriJan1,1
#716666,1152722146880749719_340863,FriJan1,1
#8B7D7D,1152722080165873450_545005592,SatJan1,1
#4C3F3F,1152722094194289757_285178194,SatJan1,1
#716666,1152722146880749719_340863,SatJan1,1
```

## The square piechart
On github you can find the six square square pie chart at [6datapoints-squarepiechart.png](https://github.com/rtanglao/2016-r-rtgram/blob/master/6datapoints-squarepiechart.png)

And here is the flickr embed:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/29056444650/in/dateposted-ff/" title="6datapoints-squarepiechart"><img src="https://c3.staticflickr.com/9/8309/29056444650_5624472f95.jpg" width="500" height="500" alt="6datapoints-squarepiechart"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
