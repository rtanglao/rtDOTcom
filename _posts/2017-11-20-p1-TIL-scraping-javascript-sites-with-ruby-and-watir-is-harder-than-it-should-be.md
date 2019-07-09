---
layout: post
title: "TIL Scraping websites like London Drug's photowebsite to download all photos instead of laboriously one at a time with Ruby and Watir using Selenium is too hard."
---

## Pontifications

* I'm just trying to scrape the London Drug's photowebsite to download all photos at a time instead of laboriously one at at time.
* Watir and Ruby and Selenium are hard.
* But scraping an Angular site like LD's photo website is a nightmare.
* Firefox developer tools:
    * ```Right Click```->```Inspect Element``` and ```copy```->```Xpath``` is your friend

### Code

Here is my non working code that only gets 32 out of 37 photos:

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'watir'
require 'watir-scroll'
require 'pp'

url = "https://photolab.londondrugs.com/prints?coll=mVnr3ZX2GN3v1K46YLzyJxjo"
b = Watir::Browser.start url ,  :firefox #, headless: true
#pp b.i
b.element(:xpath => '/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[2]/div[2]/photos-view/div/div[1]/photos-toolbar/div/div[1]/div/button').wait_until_present.click
b.element(:xpath, "/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[2]/div[2]/photos-view/div/div[1]/photos-toolbar/div/div[1]/div/ul/li[2]/div[2]/span").wait_until_present.click
b.element(:xpath => '/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[2]/div[2]/photos-view/div/div[1]/photos-toolbar/div/div[1]/div/button').wait_until_present.click
b.element(:xpath, "/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[2]/div[2]/photos-view/div/div[1]/photos-toolbar/div/div[1]/div/ul/li[1]/div[2]/span").wait_until_present.click
num = b.element(xpath: "/html/body/div[2]/div[2]/div/prints/div/div/div/prints-photos/div/div/div[1]/div[1]/collections-view/div/div[1]/div[1]/div[3]/ul/li[2]/div/div[2]/div[1]")
num_photos =  num.text.to_i
$stderr.printf("num_photos:%d\n", num_photos)
done = false
urls = []
url_count = 0
Watir::Wait.until(timeout: 180) {
  $stderr.printf("LENGTH:%d\n", b.images.length)  ;
  current_length = b.images.length
  b.scroll.to :top
  b.scroll.to :bottom
  last_photo = nil;
  e = b.images.each do |i|
    src = i.src
    #pp src
    if src.include?("storage.photofinale")
      last_photo = i
      i.wait_until_present.click
      b.scroll.to :bottom
      b.scroll.to :top
      $stderr.printf("VALID URL:%s, count:%d\n", src, url_count + 1) if !urls.include?(src)
      url_count += 1 if !urls.include?(src)
      urls.push(src) if !urls.include?(src)
    end
  end;
  $stderr.printf("last photo:%s\n", last_photo.src);
  last_photo.scroll.to :top ;
  if urls.length == num_photos
    $stderr.puts("EXITING")
    done = true
  end;
  done }
urls.each do |src|
  $stderr.puts(src)
  if src.include?("storage.photofinale")
    #pp src
    original_url = src.gsub("&size=240", "&size=0")
    pp original_url
  end
end
```