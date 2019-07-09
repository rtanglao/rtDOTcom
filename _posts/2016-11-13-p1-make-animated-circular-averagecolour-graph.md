---
layout: post
title: How to make an Animated Circular Graph in R
---
## Pontifications

* ```colours360``` is a data frame with hex colours e.g. #f72738
* ```axes = F``` means don't draw any X or Y axis tick marks; this combined with setting ```main```, ```xlab```, ```ylab``` to ```""``` results in a void theme i.e. a blank graph with just the graphics!
* ```lwd = 30``` means line width of 30 units
* [draw.radial.line documentation](http://search.r-project.org/R/library/plotrix/html/draw.radial.line.html)
* full details: [https://github.com/rtanglao/rt-animated-gifs](https://github.com/rtanglao/rt-animated-gifs) Scroll down to [November 13, 2016](https://github.com/rtanglao/rt-animated-gifs#november-13-2016)

### Code

```R
library(plotrix)

plot(0, xlim=c(1,5), ylim=c(1,5), main="", xlab="",
  ylab="", type="n", axes=F)
index = 0
for (row in 1:nrow(colours360)) {
  draw.radial.line(0,2,deg= index, center=c(3,3), 
    col= colours360[row,], expand = FALSE, lwd = 30)
  Sys.sleep(0.25) #sleep for 1/4 of a second
  index = index + 1
}
```

### Twitter compatible animated GIF output

![512x512-first360-images-average-colour-roland-flickr-2004](https://c2.staticflickr.com/6/5629/30973347135_f3fe4a400c_o_d.gif)
