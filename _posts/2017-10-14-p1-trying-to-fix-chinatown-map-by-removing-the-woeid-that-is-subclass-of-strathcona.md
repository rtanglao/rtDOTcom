---
layout: post
title: "Trying to fix Chinatown map that is only two points by removing outlier points that are in the Chinatown woeid that's a subclass of Strathcona"
---

## Pontifications

* 1\. [From the last post](http://rolandtanglao.com/2017/10/12/p1-maps-of-vancouver-neighourhoods-average-colour-instagram/), I found out that Chinatown map was blank:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36957069814/in/dateposted-public/" title="Chinatown-instagram-vancouver-2015-average-colour-overplotted"><img src="https://farm5.staticflickr.com/4480/36957069814_cb04b5afc3.jpg" width="500" height="303" alt="with-outliers-Chinatown-instagram-vancouver-2015-average-colour-overplotted"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* 2\. So [I wrote some code called remove-outliers-chinatown.rb[1]](https://github.com/rtanglao/ig-ggmap/blob/master/remove-outliers-chinatown.rb) to remove anything that isn't in woeid  ```91977405``` because apparently there's another woeid for another Vancouver Chinatown :-) (there is only one Chinatown!). This other wooed is a subwoeid of Strathcona.
* 3\. Here's how I invoked it

```R
chinatown_ig_van_2015 <-
all_neighbourhoods_ig_van_2015 %>%
filter(neighbourhood == "Chinatown")
chinatown_ig_van_2015 <-
all_neighbourhoods_ig_van_2015 %>%
filter(neighbourhood == "Chinatown")
```

```bash
cat \
WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD/with_outliers_chinatown_ig_van_2015.csv |\
 ./remove-outliers-chinatown.rb \
 > WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/CHROMELESS_MAPS_FOR_EACH_NEIGHBOURHOOD/with__91977405_chinatown_ig_van_2015.csv \
 2>stderr.with__91977405_chinatown_ig_van_2015.txt
```

* 4\. Next up is plotting: 
```with\__91977405_chinatown_ig_van_2015.csv``` (which due to a bug or a network timeout only goes from Jan 1, 2015 until December 5, 2015)

### [1] remove-outliers-chinatown.rb

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'parseconfig'
require 'pp'
require 'typhoeus'
require 'json'

def getFlickrResponse(url, params)
  url = "https://api.flickr.com/" + url
  result = Typhoeus::Request.get(url,
             :params => params )
  return JSON.parse(result.body)
end

flickr_config = ParseConfig.new('flickr.conf').params
api_key = flickr_config['api_key']

# pp api_key

first = true
ARGF.each do |line|
  if first
    first = false
    printf("colour,lat,long,date,neighbourhood\n")
    next
  end
  averagecolour_lat_lon_date = line.chomp
  fields = averagecolour_lat_lon_date.split(',')
  lat = fields[1]
  lon = fields[2]

  base_url = "services/rest/"
  
  url_params = {:method => "flickr.places.findByLatLon",
      :api_key => api_key,
      :format => "json",
      :nojsoncallback => "1",
      :lat => lat,
      :lon => lon
    }
  woeid_rsp = getFlickrResponse(base_url, url_params)
  PP::pp(woeid_rsp, $stderr)
  
  place = woeid_rsp["places"]["place"]
  if place == []
    $stderr.printf("place is nil, skipping\n")
    next
  end
  
  woeid =  place[0]["woeid"]
  if woeid != "91977405"
    $stderr.printf("WOEID is %s, SKIPPING\n", woeid)
    next
  end
  puts(line)
  sleep(0.5)
  
end

```