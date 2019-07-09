---
layout: post
title: "MongoDB query to export Firefox unanswered questions into a CSV file "
---

## Pontifications

* 1\. MongoDB query to get Firefox unanswered questions into a CSV file (I used 3T MongoChef to run the query and export to CSV; you can also export to JSON), result is in [firefox\_desktop\_only\_not\_answered\_in\_72hours\_id\_created.csv](https://github.com/rtanglao/sumo-questions/blob/master/firefox_desktop_only_not_answered_in_72hours_id_created.csv) :

```mongo
db.questions.find(
{"product_id":1, "answered_in_72_hours":false},
 {"id":1, "created":1, "_id":0})
```