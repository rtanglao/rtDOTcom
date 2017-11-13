---
layout: post
title: "R - ggjoy() - Successful joyplot with fill colours and colours and faceted by string colourname"
---

## Pontifications

* Colorized and filled with with colourname and faceted! 
* Next: try [faceting by the integer version of the 600 string colournames](http://rolandtanglao.com/2017/09/10/p1-faceted-daynumber-sixhundred-colurs-r-ggjoy-joyplot-with-colours-and-fill-colour/)!

## Faceted by Colourname with fill and colour: average colour instagram vancouver january 2016 aes-x-hour-y-colourname, geom_joy-scale16

* Invoked as:

```bash
cd /Users/rtanglao/Dropbox/GIT/2016-r-rtgram/JANUARY2016
Rscript ../makeZazzleGraphic-ig-van-jan2016-avg-colour-ggjoy.R &
```
(output is: ```<unix_time_in_seconds>-makeZazzleGraphic-ig-van-jan2016-avg-colour-ggjoy.png```)

From [https://github.com/rtanglao/2016-r-rtgram/blob/master/makeZazzleGraphic-ig-van-jan2016-avg-colour-ggjoy.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/makeZazzleGraphic-ig-van-jan2016-avg-colour-ggjoy.R)

```R
library(tidyverse)
library(plotrix)
library(ggjoy)
library(R.utils)

args <- commandArgs(asValue=TRUE)

main <- function() {

  csv_url = 
    "https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"
  
  average_colour_ig_van_jan2016 = 
    read_csv(csv_url)
  
  colour_named_vector <-
    setNames(as.character(average_colour_ig_van_jan2016$colourname), 
             average_colour_ig_van_jan2016$colourname)
  p =
    ggplot(average_colour_ig_van_jan2016, aes(x=hour, y= colourname , height=..density..))+
    geom_joy(scale=16, aes(colour=colour_named_vector, fill=colour_named_vector)) +
    scale_colour_manual(values=colour_named_vector)+ 
    scale_fill_manual(values=colour_named_vector)+
    theme_void()+theme(legend.position = 'none') +
    theme(strip.background = element_blank(),strip.text.x = element_blank())+
    facet_wrap(~ daynumber, nrow = 1) 
  
  filename = sprintf("%d-%s", as.integer(Sys.time()),gsub("R", "png", basename(args$file)))
  
  ggsave(filename,
         p,
         width = 14,
         height = 12,
         dpi = 150,
         limitsize = FALSE) #multiply height and width by dpi to get px
  
}

sink("log.txt")
main()
sink()
```

### Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36973527711/in/datetaken-public/" title="for zazzle 1504931568-makeZazzleGraphic-ig-van-jan2016-avg-colour-ggjoy"><img src="https://farm5.staticflickr.com/4438/36973527711_23ca44fd20.jpg" width="500" height="429" alt="for zazzle 1504931568-makeZazzleGraphic-ig-van-jan2016-avg-colour-ggjoy"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>