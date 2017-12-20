---
layout: post
title: "How To: Make Word Clouds in Ruby"
---

## Pontifications

* 1\. Setup magic_cloud, from [https://stackoverflow.com/questions/22715738/imagemagick-error](https://stackoverflow.com/questions/22715738/imagemagick-error) :

```bash
https://stackoverflow.com/questions/22715738/imagemagick-error
brew uninstall imagemagick@6 
brew install imagemagick@6 
PKG_CONFIG_PATH=/usr/local/opt/imagemagick@6/lib/pkgconfig gem install rmagick
```

* 2\. make word cloud

```bash
../print-out-words-from-questions-questions.rb ff55-56-question_questions.csv >ff55-ff56-unanswered-questions.txt
magic_cloud --textfile ff55-ff56-unanswered-questions.txt -f naive-ff55-ff56.jpg
```

* 3\. Output
![Naive 55-56 wordcloud](https://raw.githubusercontent.com/rtanglao/sumo-questions/master/SUMO-QUESTIONS_MYSQL_20OCT2017/naive-ff55-ff56.jpg)