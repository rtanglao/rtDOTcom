---
layout: post
title: "Null array error check added to: Ruby version of getting neighbourhood aka woe_name from lat/lon of instagram 2015 data"
---

## Pontifications

* See ["Ruby version of getting neighbourhood aka woe_name from lat/lon of instagram 2015 data"](http://rolandtanglao.com/2017/09/19/p1-ruby-version-of-add-neighbourhood-aka-woename-to-lat-lon/).
* The difference is the following null array check was added:

```ruby
place = woeid_rsp["places"]["place"]
if place == [] # null array check starts here
  $stderr.printf("place is nil, skipping\n")
  next
end
  
woe_name =  place[0]["woe_name"]
```

* See code below
* Code is invoked as:

```bash
cat \
~/Downloads/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv \
| ./add-neightbourhood-to-csv.rb \
> 13March2016-instagram-vancouver-top-colour-lat-long-date-neighbourhood-2015.csv
```

where:

 * ```~/Downloads/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv``` is the unzipped version of: [https://github.com/rtanglao/rtgram/blob/master/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv.gz](https://github.com/rtanglao/rtgram/blob/master/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv.gz)
    
  * and ```api_key``` is ```Key:``` from: [https://www.flickr.com/services/apps/72157622539864558/key/](https://www.flickr.com/services/apps/72157622539864558/key/)


### Code

copied and pasted from: [https://github.com/rtanglao/ig-ggmap/blob/master/add-neightbourhood-to-csv.rb](https://github.com/rtanglao/ig-ggmap/blob/master/add-neightbourhood-to-csv.rb)

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

first = TRUE
ARGF.each do |line|
  if first
    first = FALSE
    printf("colour,lat,long,date,neighbourhood\n")
    next
  end
  averagecolour_lat_lon_date = line.chomp
  fields = averagecolour_lat_lon_date.split(',')
  lat = fields[1]
  lon = fields[2]

  #$stderr.printf("number of fields:%d\n", fields.length)
  #exit

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
  
  woe_name =  place[0]["woe_name"]

  printf("%s,%s\n",  averagecolour_lat_lon_date, woe_name)
  sleep(0.5)
end
```
