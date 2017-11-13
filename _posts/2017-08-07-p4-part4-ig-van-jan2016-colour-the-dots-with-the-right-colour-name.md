---
layout: post
title: "Part 4 - mpg scatterplot - applied to average colour instagram by hour jan 1-31, 2016 - colour the dots correctly instead of making them all black"
---

## Pontifications

* [Part 1](http://rolandtanglao.com/2017/08/07/p1-mpg-scatterplot-average-colour-instagram-r-data-science/), [Part 2](http://rolandtanglao.com/2017/08/07/p2-part2-create-csv-files-with-plotrix-colour-names/), [Part 3](http://rolandtanglao.com/2017/08/07/p3-part3-create-naive-scatterplot-with-colournames/)
* First, here's the output. The difference from part 3 is the dots are not all black but instead their actual colour, average colour, from the colourname column:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/35629942613/" title="part4-colourname-aesthetic-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname"><img src="https://farm5.staticflickr.com/4416/35629942613_f1896066a1_n.jpg" width="320" height="174" alt="part4-colourname-aesthetic-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>


* Here's the relevant code from [https://github.com/rtanglao/2016-r-rtgram/blob/master/part4-create-colourname-with-colourname-aesthetic-scatterplot-hour.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/part4-create-colourname-with-colourname-aesthetic-scatterplot-hour.R) : 

```R
csv_url = "https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv"
average_colour_ig_van_jan2016_colourname = read_csv(csv_url)
plot =
    ggplot(data=average_colour_ig_van_jan2016_colourname)+
geom_point(colour=average_colour_ig_van_jan2016_colourname$colourname, mapping = aes(x = hour, y=colourname))
```

* All the dots are now the correct colour!
* If you put the ```colour=average_colour_ig_van_jan2016_colourname$colourname``` in the ```mapping = aes``` section instead of the ```geom_point``` section the colours will be **mapped** to levels and the actual color names won't be used!
* This RScript was invoked as follows:

```bash
cd JANUARY2016
Rscript ../part4-create-colourname-with-colourname-aesthetic-scatterplot-hour.R
```

* In [Part 5](http://rolandtanglao.com/2017/08/07/p5-part5-ig-van-jan2016-chromeless-big-dots/), we'll try and create "art" :-)  by adding ```theme_void()``` and removing all chrome from the plot!