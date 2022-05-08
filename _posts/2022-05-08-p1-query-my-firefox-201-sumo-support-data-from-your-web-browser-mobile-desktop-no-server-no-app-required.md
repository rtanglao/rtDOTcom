---
layout: post
title: "Thanks to Simon Willison's lite.datasette.io you can now query any SQLite data with CORS headers anywhere and share the query URL with others so it can spread virally :-)!  (e.g. 2021 Firefox SUMO Support questions) on any web browser including desktop, iOS and Android" 
---

* See Simon's Datasette Lite announcement blog post: [Datasette Lite: a server-side Python web application running in a browser](https://simonwillison.net/2022/May/4/datasette-lite/)

* Sample queries using lite.datasette.io and the SUMO Firefox 2021 Desktop Support Question SQLite database at: [https://rtanglao.github.io/rt-kits-api3/YEARLY_CSV_FILES/2021-firefox-sumo-questions.db](https://rtanglao.github.io/rt-kits-api3/YEARLY_CSV_FILES/2021-firefox-sumo-questions.db)

* How to use it:

  * 1. Surf to [lite.datasette.io](https://lite.datasette.io)
    2. Click `Load database by URL to a SQLite DB` and enter `https://rtanglao.github.io/rt-kits-api3/YEARLY_CSV_FILES/2021-firefox-sumo-questions.db` or any other URL of a SQLite file with CORS headers ---> Simon wrote: `You can instead use the “Load database by URL to a SQLite DB” button to  paste in a URL to your own database. That file will need to be served  with CORS headers that allow it to be fetched by the website` ([see README](https://github.com/simonw/datasette-lite/#opening-other-databases)).
    3. Click on the relevant table e.g. in this case `2021-yearly-ff-questions-en-us` and then Enter your queries using SQLite's SQL. Each query will have a unique URL which you can share with others who can learn from it and do their own queries.
    4. Fame and fortune :-)

* Previously: February 21, 2021: [Everything in SQLite and Datasette and perhaps Glitch?](http://rolandtanglao.com/2021/02/21/p1-everything-in-sqlitite-and-glitch/)        

### Sample queries
From the twitter thread: [https://twitter.com/rtanglao/status/1522384229966835712](https://twitter.com/rtanglao/status/1522384229966835712)

1. How many Firefox Desktop SUMO questions in English were asked by Windows users in 2021? Answer: 16501
```sql
select count(id) from [2021-yearly-ff-questions-en-us] where tags like "%windows-%"
```
2. How many Firefox Desktop SUMO questions in English were asked by Linux users in 2021? Answer: 1601  
```sql
select count(id) from [2021-yearly-ff-questions-en-us] where tags like "%linux%"
```
2. How many Firefox Desktop SUMO questions in English were asked by Linux users in 2021? Answer: 25 (although I'm sure lots of the 1601"linux" users were ubuntu users!) 
```sql
select count(id) from [2021-yearly-ff-questions-en-us] where tags like "%ubuntu%"
```

3. How many Firefox SUMO support questions mentioned the word `virus`? Answer 37. Editorial :-) ---> AV is such a waste! Please use what's built into Windows or macOS or switch to Linux :-) Educated guess, based on working on Firefox support for >5 years, is that at least 10x or more people have an antiv*rus issue which cause them to stop using Firefox.
```sql
select * from [2021-yearly-ff-questions-en-us] 
where tags like "%virus%" or title like "%virus%" 
order by id
```