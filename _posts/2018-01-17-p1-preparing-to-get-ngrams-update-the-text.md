---
layout: post
title: "Part 1: Getting SUMO ngrams for Firefox releases: first update the question title and description"
---

## Pontifications

### Update title and content

* As part of preparing to get SUMO [ngrams](http://rolandtanglao.com/2018/01/03/p1-ngrms-bigrams-trigrams-stopword-removal-python-nltk/) for Firefox releases: first update the question title and description.
The following is from [the sumo-questions README](https://github.com/rtanglao/sumo-questions/blob/master/README.md):

* 1\. run mongodb

```bash
cd /Users/rtanglao/Dropbox/GIT/sumo-questions/MONGODB
mongod --config /usr/local/etc/mongod.conf --dbpath=. &
```

* 2\. fix firefox 55 and 56 desktop questions 

```bash
. setupMongo
cat SUMO-QUESTIONS_MYSQL_20OCT2017/ff55-56-question_questions.csv | ./add-questions-to-mongodb.rb 
```

* 3\. add firefox 57 desktop questions 

```bash
. setupMongo
cat SUMO_QUESTIONS_MYSQL_FF57_15DEC2017/ff57-questions_question.csv | ./add-questions-to-mongodb.rb 
```

### Then in part 2 we will get the raw question title and description from mongodb

* And then run it through the NLTK ngram library
    * perhaps [this NLTK tutorial (chapter 3 of the NLTK book) on cleaning raw text from the Project Gutenberg](http://www.nltk.org/book/ch03.html) will help
