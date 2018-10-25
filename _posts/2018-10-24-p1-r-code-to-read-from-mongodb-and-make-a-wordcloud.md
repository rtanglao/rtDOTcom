---
layout: post
title: "TIL: how to search and replace in a R, how to read MongoDB from R and how to make a wordcloud in R"
---

## Pontifications

* Mongodb times were weird and having to use ```$date``` with R unlike the mongodb ruby driver was also weird.
* Time in general was a nightmare to go from local Pacific time to UTC
* Finally it's the whole SVG to PNG dance is always weird; I punted by doing a screenshot in Firefox.
* Anyhow the code is called: [23october2018-wordcloud-ff63.r](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/23october2018-wordcloud-ff63.r) 
* ToDo: remove Firefox, Firefox versions, ff, and numbers and other stop words

```r
library(mongolite)
library(tidyverse)
library(textclean)
library(tidytext)
library(wordcloud2)
m <- mongo("questions",
           url = "mongodb://127.0.0.1:27017/ff62questions")
MIN_DATE = strptime("2018-10-23 00:00:00 -0700", format = '%Y-%m-%d %H:%M:%S %z',
                    tz = "UTC")
MIN_DATE_STR = strftime(MIN_DATE, "%Y-%m-%dT%H:%M:%SZ", 'UTC')
MAX_DATE = strptime("2018-10-23 23:59:59 -0700",  format = '%Y-%m-%d %H:%M:%S %z',
                    tz = "UTC")
MAX_DATE_STR = strftime(MAX_DATE, "%Y-%m-%dT%H:%M:%SZ", 'UTC')
query_str =
  sprintf(
    '{ "created" : { "$gt" : { "$date" : "%s"}, "$lte" : {"$date" : "%s"}}}',
    MIN_DATE_STR,
    MAX_DATE_STR
  )

one_day_of_data_from_mongo <-
  m$find(
    query = query_str,
    fields =
      '{
    "_id" : 0,
    "id" : 1,
    "tags" : 1,
    "title" : 1,
    "content" : 1,
    "created" : 1
    }'
  )
one_day_of_data <-
  one_day_of_data_from_mongo %>%
  unite(text, title, content, sep = " ") %>% 
  mutate(text = replace_html(text)) %>% 
  mutate(text  = str_replace_all(
    text, pattern = '[bB]ookmark?s', replacement = 'bookmark')) %>%
  mutate(text  = str_replace_all(
    text, pattern = '[fF]irefox', replacement = '')) 

tidy_23oct <-
  one_day_of_data %>%
  unnest_tokens(word, text) 
data(stop_words)
tidy_23oct <-
  tidy_23oct %>%
  anti_join(stop_words)
tidy_23oct <-
  tidy_23oct %>%
  count(word, sort = TRUE)
top150 <- head(tidy_23oct, 150)
names(top150) <- c("word", "freq")
wordcloud2(top150)
# can't export to PNG, it's just SVG but luckily in R studio you can open in firefox and take a screenshot
# issue is here for this png export bug https://github.com/Lchiffon/wordcloud2/issues/8
  
```

### 23October2018 Day 1 of Firefox 63 WordCloud Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/44821741664/in/dateposted-ff/" title="24october2018-wordcloud-screenshot-firefox62-day1-23oct2018"><img src="https://farm2.staticflickr.com/1962/44821741664_56a6cab3ae.jpg" width="500" height="350" alt="24october2018-wordcloud-screenshot-firefox62-day1-23oct2018"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>