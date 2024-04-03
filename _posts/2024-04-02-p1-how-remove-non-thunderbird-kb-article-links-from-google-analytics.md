---
layout: post
title: "How To: Remove non Thunderbird Knowledge Base Articles From Google Analytics page view report CSV using 2 Kitsune API calls to get en-US TB URLs and scraping using Mechanize to get the localized URLs"
---

1. Get the articles using the Kitsune API
   1. script: [get-all-products-kb-articles-list.rb](https://github.com/rtanglao/rt-kits-tb-api/blob/main/get-all-products-kb-articles-list.rb)
   2. unofficial but awesome API: `https://support.mozilla.org/api/1/kb/'`
2. Get the articles details using the Kitsune API
   1. script: [get-kb-article-detailed-list.rb](https://github.com/rtanglao/rt-kits-tb-api/blob/main/get-kb-article-detailed-list.rb)
   2. unofficial but awesome API: `https://support.mozilla.org/api/1/kb/#{slug}`
3. Remove all non Thunderbird Desktop articles from the article details of step 2 using [miller](https://miller.readthedocs.io/en/latest/) aka `mlr` a simple [regular expression](https://miller.readthedocs.io/en/latest/reference-main-regular-expressions/) to filter out rows that don't have `thunderbird`  in the `products_str` column
4. From 3. Get a list of TB slugs `mlr --headerless-csv-output --csv cut -f slug thunderbird-kb-title-slug-all-articles-details.csv`
5. Scrape the slugs from 4 to find all the slugs of the localized articles
   1. script:  [get-localized-sumo-kb-urls.rb](https://github.com/rtanglao/rt-kits-tb-api/blob/main/get-localized-sumo-kb-urls.rb)
   2. scraping all links at  `https://support.mozilla.org/en-US/kb/#{kb_slug.chomp}/show_translations` with class: `translated_locale` so if the url path gets changed from `show_translations` to something else or if the class for each link is changed, then the script will break
6. Get the Google Analytics for all products. Requires you to be a staff member.
7. From 6. remove everything that doesn't have a slug as per 5. or doesn't have the word `thunderbird`
   1. script: [remove-non-thunderbird-lines.rb](https://github.com/rtanglao/rt-kits-tb-api/blob/main/remove-non-thunderbird-lines.rb)

## Command Line spellcraft :-)

```bash
./get-all-products-kb-articles-list.rb # 1
# the above script creates: allproducts-kb-title-slug-all-articles.csv
./get-kb-article-detailed-list.rb allproducts-kb-title-slug-all-articles.csv # 2
# resulting file is: details-allproducts-kb-title-slug-all-articles.csv 
mlr --csv filter '$products_str =~ "thunderbird"' details-allproducts-kb-title-slug-all-articles.csv \
> thunderbird-kb-title-slug-all-articles-details.csv # 3
# As a sanity check, count the number of rows
roland@Rolands-MacBook-Pro rt-kits-tb-api % mlr --csv filter '$products_str =~ "thunderbird"' then count details-allproducts-kb-title-slug-all-articles.csv                      
count
154
mlr --headerless-csv-output --csv cut -f slug thunderbird-kb-title-slug-all-articles-details.csv \
| ./get-localized-sumo-kb-urls.rb > thunderbird-localized-sumo-kb-article-slugs.csv # 5
# for #6, Get the Google Analytics for all products  you need GA access :-) and in this case I
# got the page review report for January 1, 2023 - December 31, 2023, top 5000
# which I saved as a CSV file called:
# just-pageviews-2024-04-01-GA-jan1-dec31-2023-top5000-pageviews.csv
./remove-non-thunderbird-lines.rb thunderbird-localized-sumo-kb-article-slugs.csv just-pageviews-2024-04-01-GA-jan1-dec31-2023-top5000-pageviews.csv # 7
```

## Previously
* March 26, 2024: [How To: Get all links with a CSS class and open them to find out redirects for translations of Thunderbird Knowledge Base articles using Ruby and Nokogiri](http://rolandtanglao.com/2024/03/26/p1-how-to-get-all-link-css-class-open-mechanize-ruby-nokogiri/)

## Source code because I am paranoid :-) about Github

### [get-localized-sumo-kb-urls.rb](https://github.com/rtanglao/rt-kits-tb-api/blob/main/get-localized-sumo-kb-urls.rb)

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'amazing_print'
require 'net/http'
require 'logger'
require 'mechanize'
logger = Logger.new(STDERR)
logger.level = Logger::DEBUG
mechanize = Mechanize.new
# Prior art from 2017 :-)
# https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/OTHER-LANGUAGE/get-other-language-urls.rb
puts 'en-us-slug,localized-slug'
ARGF.each_line do |kb_slug|
  kb_slug_url = "https://support.mozilla.org/en-US/kb/#{kb_slug.chomp}/show_translations"
  logger.debug "kb_slug_url #{kb_slug_url}"
  page = mechanize.get(kb_slug_url)
  page.css('.translated_locale').map { |link| link['href'] }.each do |localized_slug|
    fromuri = "https://support.mozilla.org#{localized_slug}"
    logger.debug "fromuri:#{fromuri}"
    from_uri = URI(fromuri)
    Net::HTTP.start(from_uri.host, from_uri.port, use_ssl: from_uri.scheme == 'https') do |http|
      request = Net::HTTP::Get.new from_uri.request_uri
      response = http.request request # Net::HTTPResponse object
      response_uri = response['location']
      localized_slug_after_redirect = response_uri.nil? ? localized_slug : response_uri
      puts "#{kb_slug.chomp},#{localized_slug_after_redirect}"
      sleep(1) # Keep Kitsune from throttling this script :-)
    end
  end
end
```

### [remove-non-thunderbird-lines.rb](https://github.com/rtanglao/rt-kits-tb-api/blob/main/remove-non-thunderbird-lines.rb)

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'amazing_print'
require 'logger'
require 'csv'

logger = Logger.new(STDERR)
logger.level = Logger::DEBUG

if ARGV.length != 2
  puts "usage: #{$0} <csv-file-with-tb-slugs> <csv-file-with-allproducts-ga>"
  exit
end
CSV_WITH_SLUGS = ARGV[0]
CSV_WITH_GA = ARGV[1]

slugs = CSV.parse(File.read(CSV_WITH_SLUGS), headers: true).by_col[1].map(&:downcase)
ap slugs
tb_ga_csv = []
CSV.foreach(CSV_WITH_GA, headers: true).each do |ga_line|
  ga_l = ga_line.to_hash
  ap ga_l
  next if ga_l['Page'].nil?

  page = ga_l['Page'].downcase
  tb_ga_csv.push(ga_l) if page.include?('thunderbird') || slugs.include?(page)
end
ap tb_ga_csv
ap tb_ga_csv.first
ap tb_ga_csv.first.keys

TB_GA_OUTPUT_CSV = "just-thunderbird-desktop-articles-#{CSV_WITH_GA}".freeze
CSV.open(TB_GA_OUTPUT_CSV, 'w') do |csv|
  csv << tb_ga_csv.first.keys # adds the attributes name on the first line
  tb_ga_csv.each do |hash|
    csv << hash.values
  end
end

```

