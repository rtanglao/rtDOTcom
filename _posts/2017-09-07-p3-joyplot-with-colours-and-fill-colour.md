---
layout: post
title: "R - ggjoy() - Successful joyplot with fill colours and colours"
---

## Pontifications

* Colorized and filled with with colourname! [See previous blog post](http://rolandtanglao.com/2017/09/07/p2-first-successful-joyplot/).

## with fill and colour: average colour instagram vancouver jauary 2016 aes-x-hour-y-colourname, geom_joy-scale16

```R
ggplot(average_colour_ig_van_jan2016, 
  aes(x=hour, y= colourname , height=..density..))+
  geom_joy(scale=16, 
  aes(colour=colour_named_vector, fill=colour_named_vector)) +
  scale_colour_manual(values=colour_named_vector)+
  scale_fill_manual(values=colour_named_vector)
```

### Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36956193351/in/datetaken-public/" title="with-fill-with-colours-07sept207-ggplot-average_colour_ig_van_jan2016-aes-x-hour-y-colourname-geom_joy-scale-16"><img src="https://farm5.staticflickr.com/4343/36956193351_f69a77cfe8.jpg" width="500" height="310" alt="with-fill-with-colours-07sept207-ggplot-average_colour_ig_van_jan2016-aes-x-hour-y-colourname-geom_joy-scale-16"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>