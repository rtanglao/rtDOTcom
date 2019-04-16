---
layout: post
title: "Today I learned that SQLite doesn't have array types"
---

# Pontifications

* Today I learned that [SQLite doesn't have array types](https://stackoverflow.com/questions/3005231/how-to-store-array-in-one-column-in-sqlite3); just [NULL, INTEGER, REAL, TEXT, BLOB](https://www.sqlite.org/datatype3.html).
* Therefore if I want to store json with arrays, I can
    * a) store the JSON in a blog
    * b) put the arrays in a separate table
    * c) flatten the arrays into a string or some such kludge
* I'll probably do c) first and then b) later for my [Firefox support analyst notes](http://rolandtanglao.com/2019/04/14/p1-firefox-analyst-notes-checkvist-api-sql-lite-datasette/) 