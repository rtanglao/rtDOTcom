---
layout: post
title: "Extract Month and Year from timestamp in BigQuery using CONCAT, CAST, LPAD"
---
[Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): Aug 8, 2024 00:29  [Extract Month and Year from timestamp in Bigquery - Stack Overflow](https://stackoverflow.com/questions/48206963/extract-month-and-year-from-timestamp-in-bigquery) <-- **QUOTE**: `Answering the title of the question as probably others will end up here like me looking for a way to create a YYYYMM year-month from a BigQuery timestamp. ... This is the code I ended up with in standard SQL:`

```sql
CONCAT(\
CAST(EXTRACT(YEAR from timestamp) as string), \
LPAD(CAST(EXTRACT(MONTH from timestamp) asstring),2,'0')) \
AS yearmonth
```
^^-- I'll probably need this Eines Tages!
## Previously

*  May 25, 2020: [HowTo: SQLite SQL query to get all May 1-25, 2020 Firefox desktop en-us questions that contain sync in title, content or tags columns](http://rolandtanglao.com/2020/05/25/p3-sqlite-sql-query-to-get-all-questions-01may2020-25may2020-title-tag-content-contain-sync/)
