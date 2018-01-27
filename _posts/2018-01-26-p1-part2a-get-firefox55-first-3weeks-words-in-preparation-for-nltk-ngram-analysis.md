---
layout: post
title: "Part 2A Get Firefox 55 first 3weeks' words in preparation for NLTK -ngram-analysis"
---

## Pontifications

See [Part 1: Getting SUMO ngrams for Firefox releases: first update the question title and description](http://rolandtanglao.com/2018/01/17/p1-preparing-to-get-ngrams-update-the-text/)

* 1\. remove mongodb stdout logging with:

```ruby
Mongo::Logger.logger.level = ::Logger::FATAL # http://stackoverflow.com/questions/30292100/how-can-i-disable-mongodb-log-messages-in-console
```

* 2\. create firefox 55 title + content 1 word per line for the first 3 weeks of the release (FF55 releae dat was August 8, 2017

```bash
./get_firefox_desktop_words_by_start_stop_date.rb 2017 8 8 2017 8 28 > ff55.08August2017.28august2017.1st.3weeks.title.content.txt
```
