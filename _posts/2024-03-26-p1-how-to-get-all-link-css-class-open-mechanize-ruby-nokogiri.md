---
layout: post
title: "How To: Get all links with a CSS class and open them to find out redirects for translations of Thunderbird Knowledge Base articles using Ruby and Nokogiri"
---

* [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): Mar 25, 2024. 17:40 CSS path using Firefox's inspector:  `ul.locales:nth-child(2) > li:nth-child(4) > a:nth-child(1)` is list of localizations for a SUMO KB article https://support.mozilla.org/en-US/kb/troubleshoot-mode-thunderbird/show_translations i.e. `en-US./kb/<slug>/show_translations`
* **NOT TESTED** (I'll write a follow up blog post once I have working code) -->The following is inspired by my code from 7 years ago (!) that tested SUMO KB redirects as part of our unsuccessful migration from Kitsune to Lithium. 
    * See April 5, 20217: [How to Check 6000 URLS version 2.0](http://rolandtanglao.com/2017/04/05/how-to-check-6000-redirects-version2-aka-procedural-programming-sucks/)

## The better way (discovered after the kludgy way)
* 1. one liner using the unique CSS class name for locale links which in this case is `translated_locale`:

```ruby
page = mechanize.get ARGV[0]
results  = page.css('.translated_locale').map{ |link| link['href']}
```

* 2.  And then from: https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/test-firefox-focus-android-redirects.rb open the link to see if there is a redirect.
```ruby
Net::HTTP.start(from_uri.host, from_uri.port,
                    :use_ssl => from_uri.scheme == 'https') do |http|
      request = Net::HTTP::Get.new from_uri.request_uri
      request.basic_auth userid, password
      response = http.request request # Net::HTTPResponse object
      response_uri = response['location']
```

## Kludgy initial way

```ruby
page  = mechanize.get 'https://support.mozilla.org/en-US/kb/troubleshoot-mode-thunderbird/show_translations'
page.css('.translated_locale').each do |l|
irb(main):201:1*   puts l.css('@href').first.value
irb(main):202:0> end
```

## Previously
* April 7, 2017:[What is the best open source tool to test HTTP redirects on 6000 URLs?](http://rolandtanglao.com/2017/04/07/Best-tool-to-test-HTTP-redirects/)
