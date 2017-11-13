---
layout: post
title: How to Check 6000 URLS
---

## Pontifications
* URLS URLS URLS
* URL encoding is `%xx` NOT `%xxx` for non roman character sets
 

### Code

[Here's how I used it to check redirects for 6000 urls](https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/README.md#29march2017).
From [test6000-redirects.rb](https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/test6000-redirects.rb):

```ruby
#!/usr/bin/env ruby
require 'rubygems'
# http://stackoverflow.com/questions/13822555/how-to-do-basic-authentication-over-https-in-ruby
# see also: rest-client

require 'net/http'
require 'parseconfig'
require 'pp'
require 'ccsv'

stage_config = ParseConfig.new('stage.conf').params
userid = stage_config['userid']
password = stage_config['password']
                        
header = true
Ccsv.foreach(ARGV[0]) do |values|
  if header == true
    header = false
    next
  end
  fromuri = values[3].gsub("support.mozilla.org", "support-stage.allizom.org") # column D
  from_uri= URI(fromuri)
  touri = values[6] #column G
  to_uri = URI(touri)

  Net::HTTP.start(from_uri.host, from_uri.port,
                  :use_ssl => from_uri.scheme == 'https') do |http|
    request = Net::HTTP::Get.new from_uri.request_uri
    request.basic_auth userid, password
    response = http.request request # Net::HTTPResponse object
    if response['location'] == touri
      printf("PASS,%d,%s,%s\n", response.code, fromuri, touri)
    else
      printf("FAIL,%d,%s,%s\n", response.code, fromuri, touri)
    end
  end
end
```