---
layout: post
title: "Part 5 - mpg scatterplot - applied to average colour instagram by hour jan 1-31, 2016 - remove the chrome and make the dots BIG"
---

## Pontifications

* [Part 1](http://rolandtanglao.com/2017/08/07/p1-mpg-scatterplot-average-colour-instagram-r-data-science/), [Part 2](http://rolandtanglao.com/2017/08/07/p2-part2-create-csv-files-with-plotrix-colour-names/), [Part 3](http://rolandtanglao.com/2017/08/07/p3-part3-create-naive-scatterplot-with-colournames/), [part 4](http://rolandtanglao.com/2017/08/07/p4-part4-ig-van-jan2016-colour-the-dots-with-the-right-colour-name/)
* First, here's the output. The difference from part 4 is the dots size=20 and all chrome has been removed (legends, etc) :

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36438473065/in/dateposted-ff/" title="size20-part5-colourname-chromeless-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname"><img src="https://farm5.staticflickr.com/4342/36438473065_ded41ba128_n.jpg" width="320" height="174" alt="size20-part5-colourname-chromeless-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* Here's the relevant code from [https://github.com/rtanglao/2016-r-rtgram/blob/master/part5-make-it-chromeless-ig-van-jan2016-scatterplot.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/part5-make-it-chromeless-ig-van-jan2016-scatterplot.R) : 

```R
csv_url = "https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"
average_colour_ig_van_jan2016_colourname = read_csv(csv_url)
plot =
    ggplot(data=average_colour_ig_van_jan2016_colourname)+
    geom_point(size=20,colour=average_colour_ig_van_jan2016_colourname$colourname,
               mapping = aes(x = hour, y=colourname)) +
    theme_void() +
    theme(legend.position = 'none') +
theme(strip.background = element_blank(),strip.text.x = element_blank())
```

* Here's the code to remove the chrome: ```theme_void```and ```theme(legend.position = 'none') +
theme(strip.background = element_blank(),strip.text.x = element_blank())```
* This RScript was invoked as follows:

```bash
cd JANUARY2016
Rscript ../part5-make-it-chromeless-ig-van-jan2016-scatterplot.R 
mv part5-colourname-chromeless-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.png size20-part5-colourname-chromeless-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.png
```

