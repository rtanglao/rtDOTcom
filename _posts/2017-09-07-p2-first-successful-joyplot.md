---
layout: post
title: "R - ggjoy() - First successful joyplot"
---

## Pontifications

* need to colorize with with colourname! That will be a [future blog post](http://rolandtanglao.com/2017/09/07/p3-joyplot-with-colours-and-fill-colour/) I hope!

## average colour instagram vancouver jauary 2016 aes-x-hour-y-colourname, geom_joy-scale16

```R
ggplot(average_colour_ig_van_jan2016, 
  aes(x=hour, y= colourname , 
    height=..density..))+
  geom_joy(scale=16)
```

### Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36926802862/" title="07sept207-ggplot-average_colour_ig_van_jan2016-aes-x-hour-y-colourname-geom_joy-scale-16"><img src="https://farm5.staticflickr.com/4371/36926802862_a42534037e.jpg" width="500" height="310" alt="07sept207-ggplot-average_colour_ig_van_jan2016-aes-x-hour-y-colourname-geom_joy-scale-16"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
