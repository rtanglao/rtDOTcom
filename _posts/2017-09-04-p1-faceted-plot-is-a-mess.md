---
layout: post
title: "R faceted geom_density ggplot2 corrupted is a mess aka learning experience :-)"
---

## Pontifications

* **UPDATE**: I think I figured it out. I need to remove ```n<=5``` over each 1 hour period of the 24 hour period not over the entire 24 hour time period of the data set.
* Not statistically valid :-) again :-) again :-)
* I don't like this version aesthetically, I envisioned 24 versions of [the previous blog post aka y axis limited to ```0.0012``` for hour 0](http://rolandtanglao.com/2017/09/02/p2-0.0012version-is-better-density-plot-corrupted-for-art/) but I tried to use 0.0012 and it didn't look good.
* I guess I need to look at a real density plot :-) somehow
 

### R ggplot2 geom_density() Code, no y axis limit, aes=colour (not the 600 R colours), faceted by hour, nrow = 2:

```R
library(tidyverse)
library(plotrix)

getnumericColour <-
  function(colorname) {
    colour_matrix=col2rgb(colorname)
    return(as.numeric(colour_matrix[1,1]) * 65536 +
             as.numeric(colour_matrix[2,1]) * 256 +
             as.numeric(colour_matrix[3,1]))
  }
csv_url = 
"https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"

average_colour_ig_van_jan2016 = 
  read_csv(csv_url)

six_hundred_colour_ints_average_colour_ig_van_jan2016 <-
  average_colour_ig_van_jan2016 %>%
  add_count(colourname) %>%
  filter(n >5) %>%
  rowwise() %>%
  mutate(sixhundred_colourint =
    getnumericColour(colourname))
ggplot(
  six_hundred_colour_ints_average_colour_ig_van_jan2016, 
  aes(x=colour))+
  geom_density(mapping = aes(colour= colour_named_vector))+
  scale_colour_manual(values=colour_named_vector)+
  theme_void()+
  theme(legend.position = 'none') +
  theme(strip.background = element_blank(),
  strip.text.x = element_blank())+
  facet_wrap(~ hour, nrow = 2)
```

### Output:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36883741461/in/datetaken-public/" title="aes-colour-no-y-axis-limit-03september2017-facet-hour-600-colour-ig-vancouver-jan2016-average-colour"><img src="https://farm5.staticflickr.com/4394/36883741461_5a5f293577_n.jpg" width="320" height="198" alt="aes-colour-no-y-axis-limit-03september2017-facet-hour-600-colour-ig-vancouver-jan2016-average-colour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
