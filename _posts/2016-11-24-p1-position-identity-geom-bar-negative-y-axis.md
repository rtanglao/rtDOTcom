---
layout: post
title: ggplot2 - For negative y values in a bar graph use position="identity"
---

## Pontifications

* Key point for bar graphs with negative values that are on the y axis: [add ```position="identity"```](http://stackoverflow.com/questions/19481634/ggplot2-warning-stacking-not-well-defined-when-ymin-0) to ```geom_bar()``` arguments
* I don't know why we need this ```position="identity"``` :-) Probably more proof I need to understand statistics and the grammar of graphics more!

### Code

[From plot-rust-ff48-commits-insertions-negative-deletions.R](https://github.com/rtanglao/rt-ff48-rust/blob/master/plot-rust-ff48-commits-insertions-negative-deletions.R):

```R
library(ggplot2)
data22nov2016 = read.csv(file="rust-ff48-negative-deletions-insertions.csv", 
    stringsAsFactors=F)

p = ggplot(data=data22nov2016, aes(x=commit,
  y=number_of_lines, fill = type))+
  geom_bar(position="identity",
  stat="identity", width = 1)+
  theme_void()+ 
  theme(legend.position = 'none')+ 
  theme(strip.background = element_blank(),
  strip.text.x = element_blank())+
  scale_fill_manual(values=c("red", "green")) 
  
ggsave("rust-mp4-ff48-sorted-commits-insertion-negative-deletion.png",
  p, width = 29.1666666667,
  height = 25, dpi = 72, 
  limitsize = FALSE, 
  bg = "transparent") 
  #2100x1800 for zazzle
```

