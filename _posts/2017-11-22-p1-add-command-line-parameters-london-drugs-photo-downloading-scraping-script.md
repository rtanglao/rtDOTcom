---
layout: post
title: "Added url of photoset and photoset name command line parameters to London Drugs Scraping photo downloads script"
---

## Pontifications

 * See [previous London Drugs Scraping photo post](http://rolandtanglao.com/2017/11/20/p1-scraping-london-drugs-photo-urls-working/)
* I added a command line parameter for the photoset url and the photoset name

```sh
#./click-sidebar-ldphotos.rb <url> <photosetname>
~/Dropbox/GIT/rt-ldphoto/click-sidebar-ldphotos.rb https://photolab.londondrugs.com/prints?coll=NBbKxdL9GdXDmNzdGrAeQqyZ 13october2017-3rdsunday
```

### Code

Here is my [working code, click-sidebar-ldphotos.rb,](https://github.com/rtanglao/rt-ldphoto/blob/master/click-sidebar-ldphotos.rb) has the two new command line parameters:

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'watir'
require 'pp'
require 'curb'
require 'rack'

url = ARGV[0]
$photoset_name = ARGV[1]

def fetch_1_at_a_time(urls)
  
  i = 0
  
  easy = Curl::Easy.new
  easy.follow_location = true

  urls.each do |url|
    i += 1
    
    easy.url = url
    uri = URI.parse(url)
    params = Rack::Utils.parse_query URI(url).query
    filename = sprintf("%s-ldphoto-%3.3d-%s.jpg", $photoset_name, i, 
                       params["photo"])
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