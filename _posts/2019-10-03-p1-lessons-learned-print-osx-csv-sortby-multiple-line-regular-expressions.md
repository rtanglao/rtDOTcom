---

layout: post
title: "Create CSV file from API Ruby Lessons learned: multiple line regular expressions and sort arrays with sort_by() "
---

# Pontifications

* Lessons learned from [print-desktop-en-us-osx-increasing-ids-time-url-title-content.rb](https://github.com/rtanglao/rt-kits-api2/blob/master/print-desktop-en-us-osx-increasing-ids-time-url-title-content.rb):
* 1. use ```sort_by()``` to sort e.g.

```ruby
# ascending sort an array of arrays by the id which is the first element of each array
sorted_array =  
id_time_url_title_content_tags_array.sort_by { |h| h[0] } 
```
* 2.  multi-line regular expressions use ```/``` and ````/x``` e.g.

```ruby
osx_regexp= 
/
  (os\sx|mojave|catalina|macos|elcapitan|osx|mac\sos|
  	el\scapitan|sierra|yosemite|mavericks|
    macbook|imac|powermac|macpro|mac\spro|macintosh)
/x
```

### How to use the above script

```bash
cd 201907
../get-questions-for-1-month.rb 2019 7
../print-desktop-en-us-osx-increasing-ids-time-url-title-content.rb  \
2019-07-firefox-desktop-all-locales.csv  2>/tmp/foo.txt
```
### Code

```ruby
#!/usr/bin/env ruby
require 'json'
require 'rubygems'
require 'awesome_print'
require 'json'
require 'time'
require 'date'
require 'csv'
require 'logger'
require 'nokogiri'

logger = Logger.new(STDERR)
logger.level = Logger::DEBUG

if ARGV.length < 1
  puts "usage: #{$0} [sumoquestions.csv]"   
  exit
end

FILENAME = ARGV[0]
osx_regexp_tags = 
/
  (?:os-x|mojave|catalina|macos|elcapitan|osx|mac-os|\
  	el-capitan|sierra|yosemite|mavericks)
/x
osx_regexp= 
/
  (os\sx|mojave|catalina|macos|elcapitan|osx|mac\sos|
  	el\scapitan|sierra|yosemite|mavericks|
    macbook|imac|powermac|macpro|mac\spro|macintosh)
/x
num_osx_questions  = 0
id_time_url_title_content_tags_array = []
CSV.foreach(FILENAME, :headers => true) do |row|
  hash = {}
  content = ""
  logger.debug row['tags']
  logger.debug row['title']
  next if row['locale'] != "en-US" || row['product'] != 'firefox'
  found_in_title_or_content = false
  if osx_regexp.match(row['title']) 
  	logger.debug "FOUND os x in title"
  	found_in_title_or_content = true
  end	
  
  if !found_in_title_or_content 
  	content  = Nokogiri::HTML.fragment(row['content']).text 
  	logger.debug 'CONTENT:' + content
  	if osx_regexp.match(content) 
  		logger.debug "FOUND os x in content"
  		found_in_title_or_content = true
  	end
  end
  next if !osx_regexp_tags.match(row['tags']) if !found_in_title_or_content
  num_osx_questions += 1

  id_time_url_title_content_tags_array.push(
    [
      row['id'].to_i,
      Time.at(row["created"].to_i).strftime("%-m/%-d/%Y %H:%M:%S"), # 10/2/2019 20:34:35
      "https://support.mozilla.org/questions/" + row['id'].to_s,
      row['title'],
      content[0..79],
      row["tags"]
    ])
end
logger.debug 'num_osx_questions:' + num_osx_questions.to_s
sorted_array =  id_time_url_title_content_tags_array.sort_by { |h| h[0] }
headers = ['id', 'created', 'url', 'title', 'content', 'tags']

FILENAME = sprintf("sorted-osx-desktop-en-us-%s", ARGV[0])
CSV.open(FILENAME, "w", write_headers: true, headers: headers) do |csv_object|
  sorted_array.each {|row_array| csv_object << row_array }
end
```

