---
layout: post
title: "ggplot2 ggalt geom_encircle() sample plot of average colour"
---
* Given a CSV file saved to `~/Documents/sample-hour-count-colorname.csv` 
```csv
hour,count,colour
1,5,red
1,2,green
2,10,red
2,3,blue
3,2,green
3,5,red
```
* Then the following R code creates an encircled plot

```r
hh = read_csv("~/Documents/sample-hour-count-colorname.csv")
gg <- ggplot(hh, aes(hour, count))
p <- gg + geom_encircle(aes(group=colour,colour=I(colour))) + geom_point()
p
```
results in the following output graph

## Graph (has flickr embed which could break in the future)

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51425348981/in/datetaken-public/" title="hour-count-colour-sample-plot-averagecolour"><img src="https://live.staticflickr.com/65535/51425348981_46dded81a9.jpg" width="417" height="500" alt="hour-count-colour-sample-plot-averagecolour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## Previously         
* [Fragment:  Tools of Production – ggalt and encircling scatterplot points in R,  ggplot2 and Python <--- geom_encircle() looks great to circle photos  average colour?!? also geom_lollipop and dumbell! both look useful](http://rolandtanglao.com/2021/08/17/p1-fragment-ggalt-ggpolot2-scatterplot-geom-encircle-geom-lollipop-dumbell/)        
