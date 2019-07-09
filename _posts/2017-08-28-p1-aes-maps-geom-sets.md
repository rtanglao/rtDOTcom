---
layout: post
title: "AES maps to levels which map to the default colour palette, geom SETS"
---

## Pontifications

* As an aid to debugging the density plot with spikes of 1.0, I wanted to set the colours.
* I tried aes but that doesn't work!
* [AES maps but doesn't SET part 8888](http://rolandtanglao.com/2015/05/07/p1-aes-maps-geom-sets/) :-) the colour instead it maps the variable, in this case colourname, to a set of levels and the levels are mapped to a default colour palette i.e. the plot shows up not in the colours of colourname but in the default colour palette! Code:
```
ggplot(average_colour_ig_van_jan2016_colourname,
aes(colourname, colour=colourname)) + geom_density()
```

And here's how it looks
<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36046136364/in/datetaken/" title="ggplot(average_colour_ig_van_jan2016_colourname, aes(colourname, colour&#x3D;colourname)) + geom_density()-mapping-colourname-instead-of-plotting-colourname"><img src="https://farm5.staticflickr.com/4378/36046136364_6fe52d956e_n.jpg" width="320" height="198" alt="ggplot(average_colour_ig_van_jan2016_colourname, aes(colourname, colour&#x3D;colourname)) + geom_density()-mapping-colourname-instead-of-plotting-colourname"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>