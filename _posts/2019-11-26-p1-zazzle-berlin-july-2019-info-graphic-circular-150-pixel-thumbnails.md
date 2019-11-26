---

layout: post
title: "Zazzle infographic from Berlin July 2019 - 150px circular thumbnail from 168 thumbnails (12x14 = 1800px2100px)"
---

# Pontifications

* Recall that [Zazzle's tshirt graphic size is 1800 pixels by 2100 pixels](http://rolandtanglao.com/2016/11/25/p1-zazzle-custom-tshirt-graphic-size/)
* The  [get-thumbnail-150-berlin-2019.rb](https://github.com/rtanglao/rt-berlin-july-2019/blob/master/get-thumbnail-150-berlin-2019.rb) script is a re-do of  g[et-gallery-photo-metadata.rb](https://github.com/rtanglao/neon-for-stephanie/blob/master/get-gallery-photo-metadata.rb) with `photosets` instead of flickr `galleries` and without  `mongodb` and just getting 150 pixel by 150 px thumbnails which in the flickr API is `url_q`
* The backup script, [backup150x150.rb](https://github.com/rtanglao/rt-berlin-july-2019/blob/master/backup150x150.rb) is straightforward adaptation of what I've done before e.g. [backup-originals.rb](https://github.com/rtanglao/neon-for-stephanie/blob/master/backup-originals.rb) but again without `mongodb`

##  get-thumbnail-150-berlin-2019.rb

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'json'
require 'pp'
require 'time'
require 'date'
require 'parseconfig'
require 'typhoeus'
require 'awesome_print'

flickr_config = ParseConfig.new('flickr.conf').params
api_key = flickr_config['api_key']

if ARGV.length < 1
  puts "usage: #{$0} [setid]"
  exit
end

def getFlickrResponse(url, params, logger)
  url = "https://api.flickr.com/" + url
  try_count = 0
  begin
    result = Typhoeus::Request.get(url,
                                 :params => params )
    x = JSON.parse(result.body)
logger.debug x.ai
   #logger.debug x["photos"].ai
  rescue JSON::ParserError => e
    try_count += 1
    if try_count < 4
      $stderr.printf("JSON::ParserError exception, retry:%d\n",\
                     try_count)
      sleep(10)
      retry
    else
      $stderr.printf("JSON::ParserError exception, retrying FAILED\n")
      x = nil
    end
  end
  return x
end

logger = Logger.new(STDERR)
logger.level = Logger::DEBUG


extras_str = "url_q"

SET_ID = ARGV[0]

search_url = "services/rest/"

first_page = true
photos_per_page = 0
page = 0
photo_number = 0

while true
  url_params = {
    :method => "flickr.photosets.getPhotos",
    :api_key => api_key,
    :format => "json",
    :nojsoncallback => "1",
    :per_page     => "500",
    :photoset_id => SET_ID,
    :extras =>  extras_str,
    :sort => "date-taken-asc",
    :page => page.to_s
  }
  photos_on_this_page = getFlickrResponse(search_url, url_params, logger)
  if first_page
    first_page = false
    logger.debug photos_on_this_page["photoset"]["pages"]
    number_of_pages_to_retrieve = photos_on_this_page["photoset"]["pages"]
  end
  page += 1
  if page > number_of_pages_to_retrieve
    break
  end
  $stderr.printf("STATUS from flickr API:%s retrieved page:%d of:%d\n", photos_on_this_page["stat"],
    photos_on_this_page["photoset"]["page"], photos_on_this_page["total"].to_i)
  photos_on_this_page["photoset"]["photo"].each do|photo|
    photo["id"] = photo["id"].to_i
    id = photo["id"]
    logger.debug "PHOTO id:" + id.to_s
    logger.debug photo.ai
    photo_number += 1
    logger.debug "PHOTO number:" + photo_number.to_s
    puts(photo["url_q"])   
  end
end
```

## backup150x150.rb

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'json'
require 'curb'
require 'pp'
require 'time'
require 'date'
require 'uri'


def fetch_1_at_a_time(urls_filenames)

  easy = Curl::Easy.new
  easy.follow_location = true

  urls_filenames.each do|url_fn|
    easy.url = url_fn["url"]
    filename = url_fn["filename"]
    $stderr.print "filename:'#{filename}'"
    $stderr.print "url:'#{url_fn["url"]}'"
    if File.exist?(filename)
      $stderr.printf("skipping EXISTING filename:%s\n", filename)
      next
    end
    try_count = 0
    begin
      File.open(filename, 'wb') do|f|
        easy.on_progress {|dl_total, dl_now, ul_total, ul_now| $stderr.print "="; true }
        easy.on_body {|data| f << data; data.size }
        easy.perform
        $stderr.puts "=> '#{filename}'"
      end
    rescue Curl::Err::ConnectionFailedError => e
      try_count += 1
      if try_count < 4
        $stderr.printf("Curl:ConnectionFailedError exception, retry:%d\n",\
                       try_count)
        sleep(10)
        retry
      else
        $stderr.printf("Curl:ConnectionFailedError exception, retrying FAILED\n")
        raise e
      end
    end
  end
end

urls_filenames = []

i = 1
ARGF.each do |url|
  url = url.chomp 
  filename = sprintf("%4.4d-rt-berlin-july2019-150x-150x.jpg", i)
  next if url.nil?
  i += 1
  urls_filenames.push({"url"=> url, "filename" => filename}) 
end

$stderr.printf("FETCHING:%d originals\n", urls_filenames.length)

fetch_1_at_a_time(urls_filenames)

```
## Bash Session

```bash
mkdir 150x150
cd 150x150
# set id is: 72157709917594396 which comes from the album url:
# https://www.flickr.com/photos/roland/albums/72157709917594396
./get-thumbnail-150-berlin-2019.rb 72157709917594396 2>/tmp/log.txt >berlin2019-url-150x150.txt
cat ../berlin2019-url-150x150.txt  | ../backup150x150.rb
# 2100/150 = 14, 1800.150 = 12, 12* 14 = 168
find . -type f | shuf -n168 > rt-berlin-july2019-168files.txt 
mkdir CIRCULAR
cat rt-berlin-july2019-168files.txt | parallel magick '{}' -vignette 0x0+0+0 'CIRCULAR/{}'
cd CIRCULAR
ls -1 *.jpg > 168jpgs.txt
montage -verbose -adjoin -tile 12x14 +frame +shadow +label -adjoin -geometry '150x150+0+0<' @168jpgs.txt rt-berlin-12-14-150x150.jpg
```

