---
layout: post
title: How To -- R ggplot2 faceted plot with custom colors, no legend and no facet labels
---

tl;dr: 
```theme_void()+theme(legend.position = 'none'+
theme(strip.background = element_blank(),strip.text.x = element_blank())+ #turn off facet labels
scale_fill_manual(values=c("purple", "pink")) #hard code colours```

## Full code from github

[The code](https://github.com/rtanglao/rt-ff48-rust/blob/master/plot-rust-ff48-commits-insertions-deletions.R) is on github and the full details are in the [README](https://github.com/rtanglao/rt-ff48-rust#november-22-2016):

```R
library(ggplot2)
data22nov2016 = read.csv(file="rust-ff48-deletions-insertions.csv", 
    stringsAsFactors=F)

p = ggplot(data=data22nov2016, aes(x=commit, y=number_of_lines, fill = type))+ #must not be fill=I(type) unless type is hex colours
  geom_bar(stat="identity", width = 1)+
  facet_wrap(~type, ncol = 1)+ 
  theme_void()+ 
  theme(legend.position = 'none')+ 
  theme(strip.background = element_blank(),+
    strip.text.x = element_blank())+ #turn off facet labels
  # don't use scale_fill_manual if using fill = I(type) in aes()
  scale_fill_manual(values=c("red", "green")) #hardcode colours to red and green, 

ggsave("rust-mp4-ff48-sorted-commits-insertion-deletion.png", 
  p, width = 29.1666666667,+ 
  height = 25, dpi = 72, limitsize = FALSE,+
  bg = "transparent") #2100x1800 for zazzle
```
