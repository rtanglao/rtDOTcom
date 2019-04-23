---
layout: post
title: "How to use mlr (miller) to create an id, url CSV file from a file of ids by concatenating 'support.mozilla.org/questions/' to the id"
---

# Pontifications

```bash
mlr --csv --implicit-csv-header label id\
offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.txt\
| mlr --csv \
put '$url = "https://support.mozilla.org/questions/"\
. $id'\
> urls_offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.csv 
```

* ```offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.txt``` is just a file of 1 `id` per line
* ```mlr --csv --implicit-csv-header label id``` outputs a CSV file with one column name ```id```
* ```mlr --csv put '$url = "https://support.mozilla.org/" . $id``` adds the ```url``` column
* `.` is the string concatenation operator in miller which wasn't clear to me from the docs <--- all i could find in the docs was: "[If the regular expression is a more complex
  expression, including string concatenation using `.`,](http://johnkerl.org/miller/doc/reference.html#String_literals)"
* output is [https://github.com/rtanglao/rt-kitsune-api/blob/master/urls_offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.csv]( https://github.com/rtanglao/rt-kitsune-api/blob/master/urls_offtopic-and-duplicates-removed-01january2019-18january2019-2fa-sumo-forum-question-ids.csv)
