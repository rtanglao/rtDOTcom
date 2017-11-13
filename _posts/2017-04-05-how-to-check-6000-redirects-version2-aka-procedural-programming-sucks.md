---
layout: post
title: How to Check 6000 URLS version 2.0
---

## Pontifications
[[compare and contrast with version 1.0](http://rolandtanglao.com/2017/03/29/p1-how-to-check-6000-redirects/) and laugh !]

* Distributed systems fail and therefore checking for network problems adds lots of ugly code.
* procedural programming sucks :-)
* It shouldn't be this hard in 2017, maybe use selenium or a higher level ruby library like [rest-client](https://github.com/rest-client/rest-client)?!?
 

### Code

[Here's how I used it to check redirects for 6000 urls as of Wednesday April 5, 2017](https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/README.md#29march2017).
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
require 'openssl'

stage_config = ParseConfig.new('stage.conf').params
userid = stage_config['userid']
password = stage_config['password']

OpenSSL::SSL::VERIFY_PEER = OpenSSL::SSL::VERIFY_NONE
                        
header = true
Ccsv.foreach(ARGV[0]) do |values|
  if header == true
    header = false
    next
  end
  fromuri = values[3].gsub("support.mozilla.org", "support-stage.allizom.org") # column D
  from_uri= URI(fromuri)
  touri = values[6].gsub("support.mozilla.org", "support-stage.allizom.org") #column G
  guid_str = touri[touri.rindex("/") + 1, touri.length - 1]
  anchor_pos =  guid_str.rindex("#")
  #unless anchor_pos.nil?
  #  guid_str = guid_str[0, anchor_pos - 1]
  #end
  touri = "https://support-stage.allizom.org/t5/-/-/ta-p/" + guid_str
  to_uri = URI(touri)
  try_count = 0
  begin 
    Net::HTTP.start(from_uri.host, from_uri.port,
                    :use_ssl => from_uri.scheme == 'https',
                    :ssl_verify_mode => OpenSSL::SSL::VERIFY_NONE) do |http|
      http.verify_mode = OpenSSL::SSL::VERIFY_NONE
      request = Net::HTTP::Get.new from_uri.request_uri
      request.basic_auth userid, password
      response = http.request request # Net::HTTPResponse object
      if response.code == "301"
        $stderr.puts("in first 301")
        $stderr.puts response['location']
        $stderr.puts touri
        response_uri = response['location']
      else
        response_uri = ""
      end        
      if  response_uri == touri
        printf("PASS,%d,%s,%s\n", response.code, fromuri, touri)
      else
        printf("FAIL,%d,%s,%s\n", response.code, fromuri, response_uri)
      end
    end
  rescue Errno::ECONNRESET, Errno::ECONNREFUSED, Net::ReadTimeout, Net::OpenTimeout,
         # added SocketError based on:
         # http://stackoverflow.com/questions/3946814/handling-nethttp-get-failures
         # http://stackoverflow.com/questions/12358682/rails-post-socketerror-getaddrinfo-temporary-failure-in-name-resolution-on
         # consider adding in the future:
         # https://docs.ruby-lang.org/en/2.2.0/Resolv/DNS.html
         SocketError => e
    try_count += 1
    if try_count < 6
      $stderr.printf("%s exception, message:%s, retry:%d\n",\
                     e.class, e.message, try_count)
      sleep(10)
      retry
    else
      $stderr.printf("%s exception, message:%s, RETRY FAILED\n",\
                     e.class, e.message)
      raise e
    end
  end
end
```