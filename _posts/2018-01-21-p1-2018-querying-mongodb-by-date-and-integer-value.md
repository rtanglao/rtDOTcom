---
layout: post
title: "Querying MongodDB in 2018 using ruby and the ruby driver by date and by integer scalar value"
---

## Pontifications

* Juicy code excerpts from: [get\_firefox\_desktop_words\_by\_start\_stop\_date.rb](https://github.com/rtanglao/sumo-questions/blob/master/get_firefox_desktop_words_by_start_stop_date.rb)
    * for querying by date, see in the Code section below ```# [1]```
    * for querying by integer scalar value see ```# [2]```

### Code

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'pp'
require 'json'
require 'time'
require 'date'
require 'mongo'

MONGO_HOST = ENV["MONGO_HOST"]
raise(StandardError,"Set Mongo hostname in ENV: 'MONGO_HOST'") if !MONGO_HOST
MONGO_PORT = ENV["MONGO_PORT"]
raise(StandardError,"Set Mongo port in ENV: 'MONGO_PORT'") if !MONGO_PORT
MONGO_USER = ENV["MONGO_USER"]
# raise(StandardError,"Set Mongo user in ENV: 'MONGO_USER'") if !MONGO_USER
MONGO_PASSWORD = ENV["MONGO_PASSWORD"]
# raise(StandardError,"Set Mongo user in ENV: 'MONGO_PASSWORD'") if !MONGO_PASSWORD
QUESTIONS_DB = ENV["QUESTIONS_DB"]
raise(StandardError,\
      "Set Mongo instagram database name in ENV: 'QUESTIONS_DB'") \
  if !QUESTIONS_DB

db = Mongo::Client.new([MONGO_HOST], :database => QUESTIONS_DB)
if MONGO_USER
  auth = db.authenticate(MONGO_USER, MONGO_PASSWORD)
  if !auth
    raise(StandardError, "Couldn't authenticate, exiting")
    exit
  end
end
questionsColl = db[:questions]
if ARGV.length < 6
  puts "usage: #{$0} yyyy mm dd yyyy mmm dd -v"
  exit
end

MIN_DATE = Time.local(ARGV[0].to_i, ARGV[1].to_i, ARGV[2].to_i, 0, 0) # may want Time.utc if you don't want local time
MAX_DATE = Time.local(ARGV[3].to_i, ARGV[4].to_i, ARGV[5].to_i, 23, 59) # may want Time.utc if you don't want local time
questionsColl.find(:created => # [1]
                   {
                     :$gte => MIN_DATE,
                     :$lte => MAX_DATE },
                     :product_id => 1 # Firefox desktop is product id 1 # [2]
                  ).projection(
  {
    "id" => 1,
    "created" => 1,
    "title" => 1,
    "content" => 1,
    "product_id" => 1 
  }).each do |q|
  PP::pp(q, $stderr)
  q["title"].split(' ').each {|t| puts t}
  q["content"].split(' ').each {|c| puts c}
end

```
