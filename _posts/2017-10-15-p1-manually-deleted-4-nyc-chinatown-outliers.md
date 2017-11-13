---
layout: post
title: "Fixed Chinatown by manually deleting 4 rows that were in NYC Chinatown"
---

## Pontifications

* 1\. [From the last post, Trying to fix Chinatown map that is only two points by removing outlier points that are in the Chinatown woeid that's a subclass of Strathcona,](http://rolandtanglao.com/2017/10/14/p1-trying-to-fix-chinatown-map-by-removing-the-woeid-that-is-subclass-of-strathcona/) I realized that I could just delete all the rows manually that were in NYC Chinatown. Turns out there were only 4 NYC Chinatown rows to delete!
* [without\_nyc_chinatown\_ig\_van2015.csv](https://github.com/rtanglao/ig-ggmap/blob/master/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD/without_nyc_chinatown_ig_van2015.csv) is [with\_outliers\_chinatown\_ig\_van\_2015.csv](https://github.com/rtanglao/ig-ggmap/blob/master/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD/with_outliers_chinatown_ig_van_2015.csv) with latitude 40. i.e. nyc chinatown i.e. a total of 4 rows manually deleted, 
* The output is: [without\_nyc_chinatown\_ig\_van\_2015.png](https://github.com/rtanglao/ig-ggmap/blob/master/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD/without_nyc_chinatown_ig_van_2015.png)

### Code 

```R
without_nyc_chinatown_ig_van_2015 = 
  read.csv(file = "without_nyc_chinatown_ig_van2015.csv", stringsAsFactors = F)
ggplot(data=without_nyc_chinatown_ig_van_2015, aes(x=long, y = lat))+
  geom_point(aes(long,lat,color=I(without_nyc_chinatown_ig_van_2015$colour)),
             size=I(6.0),alpha=I(0.4))+
  theme_void()
```
  
### Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/37007000804/in/dateposted-public/" title="without_nyc_chinatown_ig_van_2015"><img src="https://farm5.staticflickr.com/4494/37007000804_482fa51665.jpg" width="500" height="309" alt="without_nyc_chinatown_ig_van_2015"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>