---
layout: post
title: "How To: Remove non Thunderbird Knowledge Base Articles From Google Analytics page view report CSV"
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
