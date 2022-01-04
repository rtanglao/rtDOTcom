---
layout: post
title:  "flickr.photos.search API change? woe_id is now woeid?"
---
* It appears the flickr search api has changed
* The official [flickr.photos.search API docs](https://www.flickr.com/services/api/flickr.photos.search.html) say `woe_id`
* And that is what I had working 12 years ago in this [gist](https://gist.github.com/rtanglao/571353#file-getgastownphotos-rb-L43)
```ruby
search_url = "/services/rest/?method=flickr.photos.search&api_key="+api_key+
      "&format=json&nojsoncallback=1&content_type="+content_type+      "&tags="+tags+"&woe_id="+woe_id+"&per_page="+per_page+"&user_id="+user_id+ "&extras="+extras+"&max_taken_date="+max_taken_date+"&page="+page.to_s
```
* `woe_id` no longer works instead you have to use it without the underscore i.e. `woeid`

* From [funwithtarry/.../gastown-backup-revolvercoffee-by-date.rb](https://github.com/rtanglao/funwithtarry/blob/main/gastown-backup-revolvercoffee-by-date.rb)
```ruby
    url_params = {:method => "flickr.photos.search",
      :api_key => api_key,
      :format => "json",
      :nojsoncallback => "1", 
      :woeid => "26332810", # gastown
      :content_type => "7", # all: photos, videos, etc
      :per_page     => "250",
      :extras =>  extras_str,
      :sort => "date-taken-asc", 
      :page => page.to_s,
      :min_taken_date => min_taken_date.to_i.to_s,
      :max_taken_date => max_taken_date.to_i.to_s,
      :tags => "revolvercoffee"
    }
```

* Previously:
  * October 2017 a post with Chinatown and Strathcona woeids: [Trying  to fix Chinatown map that is only two points by removing outlier points  that are in the Chinatown woeid that's a subclass of Strathcona](http://rolandtanglao.com/2017/10/14/p1-trying-to-fix-chinatown-map-by-removing-the-woeid-that-is-subclass-of-strathcona/)        
  * September 2017: (sadly YQL was decommissioned sometime between 2017and 2022): [Trying out YQL and flickr API for Vancouver Latitude and Longitude -> WOEID-> neighborhood name e.g. 'West End'](http://rolandtanglao.com/2017/09/17/p1-trying-out-yql-for-vancouver-latitude-longitude/)        