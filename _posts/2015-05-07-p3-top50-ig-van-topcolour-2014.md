---
layout: post
title: ggplot2&#58; working histogram plot with labels - TOP 50
---

Working R code [with labels top 50 (instead of 400) ig van 2014 top colour](https://www.flickr.com/photos/roland/17209250647/):

```r 
ggplot(sorted_top_50,aes(x=colorname,y=count))+ 
  geom_bar(colour=head(colour_hex_strings_all,50),
  stat=“identity”,fill=head(colour_hex_strings_all,
  50),width=1,position = position_dodge(width = 0.005)+
  scale_x_discrete(limits = sorted_top_50$colorname)+theme(
  axis.text.x  = element_text(angle=90, hjust=1,
  vjust=0.5,size=10))   
```                                                                                                                                                                                   