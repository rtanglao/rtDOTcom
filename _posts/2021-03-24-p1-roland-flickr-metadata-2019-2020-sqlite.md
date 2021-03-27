---
layout: post
title: "My 2019 and 2020 flickr data now available as a 2 table SQLite database. Next step:datasette real soon now :-)"
---

Previously and for more context:

* [How To retrieve flickr photos meta data in a 2021 Stylee! Been doing this since September 2010! Now with Ruby 3.0 'except'](http://rolandtanglao.com/2021/03/22/p1-getting-all-flickr-meta-data-2021-style-been-doing-this-since-2010/)
* [Everything in SQLite and Datasette and perhaps Glitch](http://rolandtanglao.com/2021/02/21/p1-everything-in-sqlitite-and-glitch/)
*  [HowTo: Datasette on Glitch for Firefox Desktop support questions January 1 to May 25, 2020](http://rolandtanglao.com/2020/05/25/p2-glitch-datasette-firefox-desktop-support-january1-may25-2020/)

## First, I created a two table SQLite database using Simon Willison's csvs-to-sqlite

* one table for `2019-roland-flickr-metadata.csv` and one table for `2020-roland-flickr-metadata.csv`

```bash
csvs-to-sqlite *.csv -dt datetaken -dt dateupload \
-dt lastupdate roland2019-2020.db
```

## Then, I uploaded it to Dropbox because at 67 Megabytes it's too large for github

* here is the home of the file on Dropbox: [https://www.dropbox.com/s/6j10e2vohp2j5kf/roland2019-2020.db?dl=0]( https://www.dropbox.com/s/6j10e2vohp2j5kf/roland2019-2020.db?dl=0)
* I think a 1 table version that includes 2019 and 2020 in 1 table instead of two is probably better? so making that next