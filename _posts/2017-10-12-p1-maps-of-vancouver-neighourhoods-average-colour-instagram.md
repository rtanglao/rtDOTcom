---
layout: post
title: "Maps of Vancouver Neighourhoods average colour over plotted"
---

## Pontifications

* Bugs in Chinatown because of multiple woeids for Chinatown? [That will be the next post](http://rolandtanglao.com/2017/10/14/p1-trying-to-fix-chinatown-map-by-removing-the-woeid-that-is-subclass-of-strathcona/) :-) 
* [33 Maps](https://github.com/rtanglao/ig-ggmap/tree/master/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD) of Vancouver Neighourhoods average colour over plotted (Gastown is the photo I chose for the set):

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/albums/72157687937284373" title="12October2017 overplotted average colour instagram vancouver 2015 by neighbourhood"><img src="https://farm5.staticflickr.com/4485/37618225306_471a96f04c.jpg" width="500" height="303" alt="12October2017 overplotted average colour instagram vancouver 2015 by neighbourhood"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* Here's how I did it:

* 1\. In R Studio:

```R
setwd("/Users/rtanglao/Dropbox/GIT/ig-ggmap/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD")
write.csv(filter_step2_ig_van_neighbourhood_2015, 
          file = "filter_step2_ig_van_neighbourhood_2015.csv",
          row.names=FALSE)
```

* 2\. from the command line, get the neighbourhoods and create a map for each:

```bash
tail -n +2 filter_step2_ig_van_neighbourhood_2015.csv |\
cut -d "," -f5 | sort | uniq -c | \
sort -rn > reverse_sorted_vancouver_neighbourhoods.txt
cp reverse_sorted_vancouver_neighbourhoods.txt \
only_real_vancouver-reverse-sortedwithout-counts.txt
vi !$ # remove non real vancouver neighbourhoods and the counts
cat only_real_vancouver-reverse-sortedwithout-counts.txt | \
parallel -N 1 \
Rscript ../../create-overplotted-Vancouver-neighbourhood-map.R {} 
```



