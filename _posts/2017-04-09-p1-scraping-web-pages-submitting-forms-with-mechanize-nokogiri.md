---
layout: post
title: Scraping web pages with ruby, mechanize and nokogiri -- How To Log in, get URL of a link and get link title
---

## Pontifications

* Helpful references: [ruby.bastardsbook:Parsing HTML with Nokogiri](http://ruby.bastardsbook.com/chapters/html-parsing/), [ruby.bastardsbook:The Mechanize Gem](http://ruby.bastardsbook.com/chapters/mechanize/), [ruby.bastardsbook:Nokogiri and CSS selectors](http://ruby.bastardsbook.com/chapters/html-parsing/), [Stack Overflow:Getting attribute's value in Nokogiri to extract link URLs](http://stackoverflow.com/questions/7107642/getting-attributes-value-in-nokogiri-to-extract-link-urls), [Crawling pages with Mechanize and Nokogiri](http://robdodson.me/crawling-pages-with-mechanize-and-nokogiri/), [HOWTO scrape websites with Ruby & Mechanize](https://readysteadycode.com/howto-scrape-websites-with-ruby-and-mechanize), [Simple way to scrape web with Ruby](http://merowing.info/2015/01/extracting-data-from-websites-without-api/)
* How to login to a website e.g. Lithium site like support.mozilla.org using mechanize:

```ruby
form = login_page.forms[1] # 2nd form on the page, search form is first
form.field_with(id: 'lia-login').value = userid # id from developer tools
form.field_with(id: 'lia-password').value = password
page = form.submit
```
* How to loop over multiple ids e.g. in this case ids of Other Languages links:

```ruby
tkb_page.css('div.tkb-other-language-link').each do |l|
  # do something
end
```
* How to get the text of link e.g. in this case the text is the name of the language e.g. Deutsch for German

```ruby
l.css('a:nth-child(1)').children.text
```
* How to get the link url:

```ruby
l.css('a:nth-child(1)/@href').first.value
```

### Full code 

From [get-other-language-urls.rb](https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/OTHER-LANGUAGE/get-other-language-urls.rb)

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'mechanize'
require 'parseconfig'
require 'pp'

stage_config = ParseConfig.new('user.conf').params
userid = stage_config['userid']
password = stage_config['password']

mechanize = Mechanize.new
login_page = mechanize.get 'https://support.mozilla.org/t5/user/userloginpage'

form = login_page.forms[1]
form.field_with(id: 'lia-login').value = userid
form.field_with(id: 'lia-password').value = password

page = form.submit

tkb_page = mechanize.get ARGV[0]
puts("POSSIBLE-locale,link")
tkb_page.css('div.tkb-other-language-link').each do |l|
  possible_locale = l.css('a:nth-child(1)').children.text
  possible_locale = "NOT en-us" if possible_locale == "English (US)"
  printf("%s,%s\n", possible_locale,
         "https://support.mozilla.org" +
         l.css('a:nth-child(1)/@href').first.value)
end
```