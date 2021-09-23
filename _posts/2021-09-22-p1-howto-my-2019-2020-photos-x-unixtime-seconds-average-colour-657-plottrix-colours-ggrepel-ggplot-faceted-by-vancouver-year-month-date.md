---
layout: post
title: "How to create an ggrepel plot of R's 657 plotrix colours of the average colour of my 2019-2020 flickr photos, x axis is time in unix seconds since 1970 using R, y axis is the average colour using the plotrix colours"
---
* tl;dr running [segment-size-1.5-infinite-overlaps-bold-no_theme_no_caption_geom_point_ggrepl_roland_flickr_2019_2020.R](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/segment-size-1.5-infinite-overlaps-bold-no_theme_no_caption_geom_point_ggrepl_roland_flickr_2019_2020.R) creates [segment-size-1.5-infinite-overlaps-bold-no_theme_no_caption_geom_point_ggrepl_roland_flickr_2019_2020.png](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/OUTPUT_GRAPHICS/segment-size-1.5-infinite-overlaps-bold-no_theme_no_caption_geom_point_ggrepl_roland_flickr_2019_2020.png)
* Repel means the labels 'repel' each other. 
* The default segment thickness is 0.5mm. I changed it to 1.5mm in the hope of a more colourful plot. Not as dramatic as I would have liked.
* Would be  cool to do this on a per day basis instead of faceted so I can control the layout precisely. e.g. do a monthly layout

## Previously

* [How  to create an encircled plot of R's 657 plotrix colours of the average  colour of my 2019-2020 flickr photos, x axis is time in unix seconds  since 1970 using ggalt and ggplot in R, y axis is the average colour  using the plotrix colours](http://rolandtanglao.com/2021/09/14/p1-howto-my-2019-2020-photos-x-unixtime-seconds-average-colour-657-plottrix-colours-encircled-ggalt-ggplot-faceted-by-vancouver-year-month-date/)      

## Code (since I don't trust github to last forever :-) 

```r
library(tidyverse)
library(ggrepel)
roland_f_2019_2020_narrow_dataset <- read_csv("https://media.githubusercontent.com/media/rtanglao/rt-flickr-sqlite-csv/main/LARGE_CSV_FILES/pacific-yyyy-mm-dd-2020-2019-roland-flickr-datetaken-synth_75sqisvalid-synth_plotrixcolour_unixtimedt.csv")
roland_flickr_20192020_average_colour_plot_colors_factor <- ggplot(roland_f_2019_2020_narrow_dataset,  aes(unixtime_dt,synth_plotrixcolour))
ggrepel_roland_flickr_20192020_average_colour_plot_colors_plot <- roland_flickr_20192020_average_colour_plot_colors_factor +
geom_point(aes(colour=I(synth_plotrixcolour)))  + 
geom_label_repel(aes(label = synth_plotrixcolour, 
  colour = I(synth_plotrixcolour)),
  vjust = "inward", hjust = "inward", fontface = "bold",
  max.overlaps = Inf,
  nudge_y = 2.5, nudge_x = -8, size = 3, segment.size = 1.5) +
facet_wrap(~ pacific_ymd, scales = "free") +
theme_void() +
theme(
    strip.background = element_blank(),
    strip.text.x = element_blank()
  )  
```

## Output (flickr embed which might also break)

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51495129323/in/photolist-2msK71G-2msrZTi-2mrBsgN-2mqhG7M-2mpxABk-2mp6gJr-2kUADFT-2kRkWcX" title="segment-size-1.5-infinite-overlaps-bold-no_theme_no_caption_geom_point_ggrepl_roland_flickr_2019_2020"><img src="https://live.staticflickr.com/65535/51495129323_2926fcc164.jpg" width="417" height="500" alt="segment-size-1.5-infinite-overlaps-bold-no_theme_no_caption_geom_point_ggrepl_roland_flickr_2019_2020"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>