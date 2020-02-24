---

layout: post
title: "SQLite, JSON, CSV :-) the eternal golden braid of formats? so many tools for normal folks to grok them without programming e.g. sqlitebrowser"
---

# Pontifications

* For many years, I thought I needed a "real" database for my hobbyist programming of tshirts and other things. So I learned and used MongoDB starting in 2011 for my Thunderbird support scripts (see [MongoDB is my current persistent data structure store of choice aka "how to slurp your Get Satisfaction data into MongoDB"](http://rolandtanglao.com/2011/04/04/mongodb-is-my-current-persistent-data-structure-store-of-choice-aka-how-to-slurp-your-get-satisfaction-data-into-mongodb/) from April 2011)
* A legacy of growing up with small files and slow disks? i.e. programming since 1977
* Anyhow it's the 21st century and you can do everything with SQLite, JSON and CSV up until about what 1-2GB per file, perhaps even larger?
* In other words, you don't need MongoDB or indeed any "real database" like PostgreSQL until you have many gigabytes of data! And most small scale projects have less than 1 GB of data in their datasets even in plain text formats like JSON and CSV and in SQLite.
* And the cool thing is SQLite, JSON and CSV can be consumed, queried and manipulated by "normal" folks without programming using Google Docs for CSV, the numerous tools for JSON and many tools for SQLite like SQLiteBrowser aka [DB Browser for SQLite](https://sqlitebrowser.org/)

