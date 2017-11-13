---
layout: post
title: "R faceted geom_density ggplot2 fixed by removing any colour that only happens <= 5 times"
---

## Pontifications

* Success, I was right [previously](http://rolandtanglao.com/2017/09/04/p1-faceted-plot-is-a-mess/) :-)
 

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

# define a function to return tibble with <=5 removed for that hour
remove_lessthan_6_for_1hour <-
  function(tibble, hour_as_string) {
    tibble %>%
      filter(hour == hour_as_string) %>%
      add_count(colourname) %>%
      filter(n >5)
}
less_than_6_removed <-
  bind_rows(
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "00"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "01"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "02"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "03"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "04"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "05"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "06"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "07"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "08"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "09"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "10"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "11"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "12"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "13"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "14"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "15"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "16"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "17"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "18"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "19"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "20"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "21"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "22"),
  remove_lessthan_6_for_1hour(average_colour_ig_van_jan2016, "23")
  )
  
sept042017_int_colour_ig_van_june2016_average_colour <-
  less_than_6_removed %>%
  rowwise() %>%
  mutate(sixhundred_colourint = getnumericColour(colourname))
colour_hex_strings_all = 
  sapply(
    sept042017_int_colour_ig_van_june2016_average_colour$sixhundred_colourint, 
      function(x){
        sprintf("#%6.6X", x)})

colour_named_vector <- 
  setNames(as.character(colour_hex_strings_all), 
           colour_hex_strings_all)

# 0.0003
ggplot(sept042017_int_colour_ig_van_june2016_average_colour, aes(x=colour))+
  geom_density(mapping = aes(colour = colour_named_vector))+
  scale_colour_manual(values=colour_named_vector)+
  scale_y_continuous(limits = c(0,0.0003))+
  theme_void()+theme(legend.position = 'none') +
  theme(strip.background = element_blank(),strip.text.x = element_blank())+
  facet_wrap(~ hour, nrow = 2)

```

### Output:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/37035623315/in/datetaken-public/" title="y-limited-0.0003-sept042017_int_colour_ig_van_june2016_average_colour"><img src="https://farm5.staticflickr.com/4420/37035623315_69ef40829f_n.jpg" width="320" height="198" alt="y-limited-0.0003-sept042017_int_colour_ig_van_june2016_average_colour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
