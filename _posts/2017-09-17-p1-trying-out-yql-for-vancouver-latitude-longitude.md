---
layout: post
title: "Trying out YQL and flickr API for Vancouver Latitude and Longitude -> WOEID-> neighborhood name e.g. 'West End'"
---

## Pontifications

* Followup from [R ggmap faceted by vancouver neighborhoods, just need lat/lon to Vancouver neighborhood function](http://rolandtanglao.com/2017/09/15/p1-ggmap-to-show-blank-spots-for-other-neighbourhoods/):
* The following YQL and REST queries gives me WOEID from lat, long, e.g. ```23405270```
* Then [find the neighborhood name from the WOEID](https://www.flickr.com/services/api/explore/flickr.places.getInfo) using this query:
```
https://api.flickr.com/services/rest/?method=flickr.places.getInfo&api_key=<api_key>&woe_id=23405270&format=json
```
* which in this case for ```23405270``` is ```place" ->"woe_name": ```West End```:

```json
jsonFlickrApi({ "place": { "place_id": "EPQ.yiVTUb7YazWQlg", "woeid": "23405270", "latitude": 49.284, "longitude": -123.135, "place_url": "\/Canada\/British+Columbia\/Vancouver\/West+End", "place_type": "neighbourhood", "place_type_id": 22, "timezone": "America\/Vancouver", "name": "West End, Vancouver, BC, CA, Canada", "woe_name": "West End", 
    "neighbourhood": { "_content": "West End, Vancouver, BC, CA, Canada", "place_id": "EPQ.yiVTUb7YazWQlg", "woeid": "23405270", "latitude": 49.284, "longitude": -123.135, "place_url": "\/Canada\/British+Columbia\/Vancouver\/West+End" }, 
    "locality": { "_content": "Vancouver, British Columbia, Canada", "place_id": "lOfvpopYWrrC", "woeid": "9807", "latitude": 49.247, "longitude": -123.106, "place_url": "\/Canada\/British+Columbia\/Vancouver" }, 
    "county": { "_content": "Greater Vancouver, British Columbia, Canada", "place_id": "emTQ4FlTW7nupnbp2Q", "woeid": "29375222", "latitude": 49.290, "longitude": -122.851, "place_url": "\/emTQ4FlTW7nupnbp2Q" }, 
    "region": { "_content": "British Columbia, Canada", "place_id": "VjS6xONTUb6pGKV0", "woeid": "2344916", "latitude": 54.498, "longitude": -126.550, "place_url": "\/Canada\/British+Columbia" }, 
    "country": { "_content": "Canada", "place_id": "b9iFoOpTUb6KZ3MPGQ", "woeid": "23424775", "latitude": 56.954, "longitude": -98.308, "place_url": "\/Canada" }, "has_shapedata": 1, 
    "shapedata": { "created": "1292367913", "alpha": 4.0690104166667E-5, "count_points": "5551", "count_edges": 38, 
      "polylines": { 
        "polyline": [
          { "_content": "49.277492523193,-123.15129089355 49.277519226074,-123.15197753906 49.282318115234,-123.1583480835 49.282531738281,-123.15948486328 49.281524658203,-123.17047119141 49.284423828125,-123.16882324219 49.287124633789,-123.16162872314 49.295913696289,-123.15330505371 49.295631408691,-123.14669799805 49.296192169189,-123.14575195312 49.296455383301,-123.14478302002 49.296722412109,-123.14395141602 49.297508239746,-123.1407699585 49.297603607178,-123.13845825195 49.297939300537,-123.13648223877 49.30078125,-123.13108825684 49.301971435547,-123.12566375732 49.300838470459,-123.11692047119 49.300834655762,-123.11683654785 49.300666809082,-123.11666870117 49.300403594971,-123.11639404297 49.300113677979,-123.1164855957 49.299156188965,-123.11682891846 49.290565490723,-123.11817932129 49.289474487305,-123.11727905273 49.289451599121,-123.11727905273 49.282867431641,-123.12403869629 49.280570983887,-123.12609863281 49.277694702148,-123.12792205811 49.274433135986,-123.13128662109 49.274452209473,-123.13172912598 49.274719238281,-123.13278961182 49.275253295898,-123.134765625 49.2751121521,-123.13733673096 49.275562286377,-123.14192199707 49.274467468262,-123.14530181885 49.277492523193,-123.15029907227 49.277492523193,-123.15129089355" }
        ] }, "has_donuthole": 0, "is_donuthole": 0, 
      "urls": { 
        "shapefile": { "_content": "http:\/\/farm6.static.flickr.com\/5085\/shapefiles\/23405270_20101214_840ec233ea.tar.gz" } } } }, "stat": "ok" })
```

### YQL

```
https://developer.yahoo.com/yql/console/#h=select+place.woeid+from+flickr.places+where+api_key+%3D++%22<api_key>%22++and+lat%3D49.285648+and+lon%3D-123.139954
```

where ```api_key``` is the ```key``` found at: [https://www.flickr.com/services/apps/72157622539864558/key/](https://www.flickr.com/services/apps/72157622539864558/key/)

### REST

(or [https://www.flickr.com/services/api/explore/flickr.places.findByLatLon](https://www.flickr.com/services/api/explore/flickr.places.findByLatLon) )

https://query.yahooapis.com/v1/public/yql?q=select%20place.woeid%20from%20flickr.places%20where%20api_key%20%3D%20%20%22<api_key%22%20%20and%20lat%3D49.285648%20and%20lon%3D-123.139954&format=json&diagnostics=true&callback=
```

### Result

```json
{
 "query": {
  "count": 1,
  "created": "2017-09-18T05:25:15Z",
  "lang": "en-US",
  "diagnostics": {
   "publiclyCallable": "true",
   "url": {
    "execution-start-time": "1",
    "execution-stop-time": "193",
    "execution-time": "192",
    "content": "https://api.flickr.com/services/rest/?method=flickr.places.findByLatLon&lat=49.285648&lon=-123.139954"
   },
   "user-time": "193",
   "service-time": "192",
   "build-version": "2.0.177"
  },
  "results": {
   "places": {
    "place": {
     "woeid": "23405270"
    }
   }
  }
 }
}
```