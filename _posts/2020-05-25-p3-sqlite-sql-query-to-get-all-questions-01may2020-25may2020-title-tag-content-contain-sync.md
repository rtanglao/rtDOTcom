---
layout: post
title: "HowTo: SQLite SQL query to get all May 1-25, 2020 Firefox desktop en-us questions that contain sync in title, content or tags columns" 
---
# Pontifications

* Here's the [SQL query](https://roland-ds1.glitch.me/data?sql=select%0D%0A++created%2C%0D%0A++url%2C%0D%0A++title%2C%0D%0A++content%2C%0D%0A++tags%0D%0Afrom%0D%0A++%5Bsorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales%5D%0D%0Awhere%0D%0A++%22created%22+%3E%3D+%3Ap2%0D%0A++and+%22created%22+%3C+%3Ap3%0D%0A++AND+%28+%22content%22+like+%3Ap0%0D%0A++or+%22tags%22+like+%3Ap4%0D%0A++or+%22title%22+like+%3Ap6%29%0D%0Aorder+by%0D%0A++rowid%0D%0Alimit%0D%0A++1000&p2=2020-04-30+16%3A00%3A00&p3=2020-05-26+00%3A00%3A00&p0=%25sync%25&p4=%25sync%25&p6=%25sync%25) from roland-ds1.glitch.me from the previous post, [HowTo: Datasette on Glitch for Firefox Desktop support questions January 1 to May 25, 2020](http://rolandtanglao.com/2020/05/25/p2-glitch-datasette-firefox-desktop-support-january1-may25-2020/)

```sql
select
  created,
  url,
  title,
  content,
  tags
from
  [sorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales]
where
  "created" >= :p2
  and "created" < :p3
  AND ( "content" like :p0
  or "tags" like :p4
  or "title" like :p6)
order by
  rowid
limit
  1000
```

where:

```sql
p2 = 2020-04-30 16:00:00
p3 = 2020-05-26 00:00:00
p0 = %sync%
p4 = %sync%
p6 = %sync%
```

And here's the [CSV file](https://docs.google.com/spreadsheets/d/18UUsBqoOk3GphPqUXQmRm98mIjX8Ut4ggatxDPZimGA/edit?usp=sharing) (as a Google Spreadsheet)