---
layout: post
title: "Learnings from R, ggmap and ggplot2: I() the as is/inhibit/insulate function"
---
Some code snippets that weren't obvious to me from reading the manual!

1. **I() - "as is" function**

If you don't use this function, ggmap, and ggplot will try <s>to make a factor</s> to use the values as names instead of using the values literally e.g.  out of your array of colours instead of using the actual hex colour values in the color column of a dataframe i.e. **color=I(data6$color)**
 
```r
f="~rtanglao/Dropbox/GIT/rtgram/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv"
data6 = read.csv(file=f,stringsAsFactors=F)
(p <- qplot(long, lat, geom = "point", data = data6,
color=I(data6$color), xlim=c(-123.27, -123.005),
ylim=c(49.21, 49.324), size=I(1.0), alpha=I(0.4))+
facet_wrap(~date) + theme_minimal())
```