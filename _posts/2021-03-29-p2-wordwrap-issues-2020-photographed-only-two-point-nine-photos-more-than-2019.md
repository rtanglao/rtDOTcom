---
layout: post
title: "2.9 times as many photos in 2020 versus 2019: Due to wordwrap/end of line issues, i took less photos than  i thought :-)"
---
* 2.9 times as many photos in 2020 compared to 2019 (36911/12638 = 2.9)

```bash
roland@Rolands-MacBook-Air THUMBS_75X75 % mlr --csv cut -f id,datetaken,url_sq \
../../files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-metadata.csv > /tmp/url_sq.txt
roland@Rolands-MacBook-Air THUMBS_75X75 % grep 2020- /tmp/url_sq.txt| wc -l
36911
roland@Rolands-MacBook-Air THUMBS_75X75 % grep 2019- /tmp/url_sq.txt| wc -l
12638
```

* demonstrates how to cut fields out of a CSV file using `mlr` aka `miller`
* Previously wrong :-) on twitter:  [I took triple the # of photos in 2020 compared to 2019! "Shutter Therapy" indeed!](https://twitter.com/rtanglao/status/1373875361512001538)