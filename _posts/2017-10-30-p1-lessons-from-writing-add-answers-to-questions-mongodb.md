---
layout: post
title: "Lessons from writing add-answers-to-questions-mongodb.rb, next time use smarter_csv and Value Converters?!?!"
---

## Pontifications

* Lessons from writing [add-answers-to-questions-mongodb.rb](https://github.com/rtanglao/sumo-questions/blob/master/add-answers-to-questions-mongodb.rb):
* 1\. in question_questions.csv: 
    * ```change "" to ","```
    * ```change "\"" to "\'"```
    * ```change "\\'", to ' "'```
* 2\. truncate the ```content``` or any large field (it seems like the built-in ruby 2.4 CSV built-in parser can't handle >256 characters and SUMO troubleshooting info can be very large i.e. 1024 characters or larger
* 3\. Next time use [https://github.com/tilo/smarter_csv](https://github.com/tilo/smarter_csv), in particular: [Value Converters](https://github.com/tilo/smarter_csv#example-6-using-value-converters) to automatically convert data fields for mongodb


### 30October2017-first-run-of-adding-answers aka replies
```bash
cat SUMO-QUESTIONS_MYSQL_20OCT2017/questions_answers.csv | 
./add-answers-to-questions-mongodb.rb
```

* 