---
layout: post
title: "Click on next photo and then download instead of scrolling is how I scraped the photos from London Drugs"
---

## Pontifications

    * See [previous London Drugs Scraping photo post](http://rolandtanglao.com/2017/11/20/p1-TIL-scraping-javascript-sites-with-ruby-and-watir-is-harder-than-it-should-be/)
* I scrapped scrolling and that works!
* Next up add a command line argument so we can do

```sh
#./click-sidebar-ldphotos.rb <url>
./click-sidebar-ldphotos.rb  https://photolab.londondrugs.com/prints?coll=mVnr3ZX2GN3v1K46YLzyJxj
```

### Code

Here is my [working code, click-sidebar-ldphotos.rb,](https://github.com/rtanglao/rt-ldphoto/blob/master/click-sidebar-ldphotos.rb) that download 37 out of 37 photos:

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'watir'
require 'pp'
require 'curb'

def fetch_1_at_a_time(urls)
  
  i = 0
  
  easy = Curl::Easy.new
  easy.follow_location = true

  urls.each do |url|
    i += 1
    
    easy.url = url
    uri = URI.parse(url)
    filename = sprintf("ldphoto-%2.2d.jpg", i)
    $stderr.print "filename:'#{filename}'"
    $stderr.print "url:'#{url}' :"
    if File.exist?(filename)
      $stderr.printf("skipping EXISTING filename:%s\n", filename)
      next
    end
  try_count = 0
    begin
      File.open(filename, 'wb') do|f|
        #easy.on_progress {|dl_total, dl_now, ul_total, ul_now| $stderr.print "="; true }
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
url = "https://photolab.londondrugs.com/prints?coll=mVnr3ZX2GN3v1K46YLzyJxjo"
b = Watir::Browser.start url ,  :firefox #, headless: true
num_path = "/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[1]/collections-view/div/div[1]/div[1]/div[3]/ul/li[2]/div/div[2]/div[1]" 
num = b.element(xpath: num_path).wait_until_present
num_photos =  num.text.to_i
$stderr.printf("num_photos:%d\n", num_photos)
urls = []
photo1 = "/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[2]/div[2]/photos-view/div/div[2]/div/ul/li[2]/ul/li[1]/div/div[1]/div[1]/div/img"
b.element(xpath: photo1).wait_until_present.click

expand_photo1 = "/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[2]/div[2]/photos-view/div/div[2]/div/ul/li[2]/ul/li[1]/div/div[1]/div[1]/div/preview-glyph/div/div/span/i[2]"

b.element(xpath: expand_photo1).wait_until_present.click
download_path = "div.commandbar-panel:nth-child(2) > photos-toolbar:nth-child(1) > div:nth-child(1) > div:nth-child(2) > div:nth-child(1) > div:nth-child(1) > a:nth-child(1)"
next_photo = "/html/body/div[2]/div[2]/div/prints-photo/div/div/div[1]/div[2]/photo-view/div/div[1]/div[5]"

loop do
  download_link = b.link(css: download_path )
  link =  download_link.href
  if !urls.include?(link)
    urls.push(link)
    $stderr.printf("ADDING:%s count:%d\n", link, urls.length)
    break if urls.length == num_photos
  end
  b.element(xpath: next_photo).wait_until_present.click
end
fetch_1_at_a_time(urls)
```