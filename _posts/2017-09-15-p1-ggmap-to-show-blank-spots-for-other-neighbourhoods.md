---
layout: post
title: "R ggmap faceted by vancouver neighborhoods, just need lat/lon to Vancouver neighborhood function"
---

## Pontifications

* Regarding [the last blog post, R ggmap faceted by vancouver neighborhoods](http://rolandtanglao.com/2017/09/13/p1-idea-ggmap-faceted-by-vancouver-neighbourhoods/), [this blog post about ggmap points to the dataset for 2015 instagram](http://rolandtanglao.com/2016/03/30/p1-r-ggmap-ggplot2-learnings/) ([dataset for 2015 vancouver instagram](https://github.com/rtanglao/rtgram/blob/master/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv.gz)). 
* All I need is a ```lat/lon -> Vancouver neighourhood/woeid function```, maybe [flickr.places.findByLatLon](https://www.flickr.com/services/api/flickr.places.findByLatLon.html)? or [using Yahoo yql](https://stackoverflow.com/a/35826094)?
* And then I will have ```n``` maps where ```n``` is the number of Vancouver neighbourhoods.