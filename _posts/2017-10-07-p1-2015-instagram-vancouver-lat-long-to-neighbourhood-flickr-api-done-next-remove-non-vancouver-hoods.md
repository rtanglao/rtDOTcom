---
layout: post
title: "Ruby script using flickr API flickr.places.findByLatLon to get neighborhood name from lat/long of instagram photos is almost done after 10 days, next: remove non-Vancouver neighourhoods"
---

## Pontifications

* [Ruby script](http://rolandtanglao.com/2017/10/04/p1-instagram-2015-lat-lon-to-neighbourhood-ruby-script-at-october-still-running-after-a-week/) [add-neighbourhood-to-csv.rb](https://github.com/rtanglao/ig-ggmap/blob/7e8b30d967b61f8e10f75491f4427125b8605714/add-neightbourhood-to-csv.rb) to get neighbourhood name from lat/long of instagram photos with the flickr API ```flickr.places.findByLatLon``` is almost done after 10 days (as of this writing at early December 2015)
* Next: Data cleaning:
    * combine the multiple cvs files into one tibble using [bind_rows()](http://rolandtanglao.com/2017/10/06/p1-combine-r-dataframes-and-tibbles-bind-row-dplyr/)
    * remove rows with non-Vancouver neighourhoods which I assume will be the outliers i.e the ones with less than 10 occurrences