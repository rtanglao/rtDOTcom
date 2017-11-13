---
layout: post
title: How To Plot radial lines in R using base graphics 
---


## Pontifications


I forgot to blog this because I found a better way to do this with ggplot2 instead of base graphics.

Anyway here's the code:

```R
index = 0
for(i in 1:nrow(colours360)) {
draw.radial.line(0, 1, 
  deg= index, center=c(3,2), 
  col=strtoi(gsub("^#", '', colours360[i,]), 16), 
    expand = TRUE)
Sys.sleep(1.0)
index = index + 1
}
```