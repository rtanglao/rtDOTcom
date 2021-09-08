---
layout: post
title: "How To: Parse Times from flickr and how to Use a specific timezone with R and lubridate e.g. `America/Vancouver` (broken in lubridate 1.7.4 to 1.7.9)"
---
* Times from flickr were in Pacific (not sure why? Maybe because I asked for it in my local time which is Vancouver time? See [How To retrieve flickr photos meta data in a 2021 Stylee! Been doing this since September 2010! Now with Ruby 3.0 'except'](http://rolandtanglao.com/2021/03/22/p1-getting-all-flickr-meta-data-2021-style-been-doing-this-since-2010/))       

```r
> x
[1] "2019-01-01 14:16:19 -0800"
> parse_date_time(x, "%Y-%m-%d %H:%M:%s %z")
[1] "2019-01-01 22:16:19 UTC"
```

## Unrecognized timezone bug in Lubridate 1.7.4 to 1.7.9 when trying to use a  specific timezone, fixed in issue 928 in 1.7.10

```r
> lubridate::with_tz(Sys.time(), "America/Vancouver")
[1] "2021-09-07 17:00:52 PDT"
Warning message:
In with_tz(x, tz) : Unrecognized time zone 'America/Vancouver'
```
* upgraded to 1.7.10 and it worked (bug was in 1.7.4 to 1.7.9 ), 
[Timezones not working since the update to R 4.0.3 #928](https://github.com/tidyverse/lubridate/issues/928) 
```r
> packageVersion("lubridate")
[1] ‘1.7.9’
> remove.packages("lubridate")
> install.packages("lubridate")
> packageVersion("lubridate")
[1] ‘1.7.10’
> lubridate::with_tz(Sys.time(), "America/Vancouver")
[1] "2021-09-07 17:29:23 PDT"
```

## Previously

* [HowTo add the 657 built in R colors to the flickr dataset (you need rowwise())](http://rolandtanglao.com/2021/04/20/p1-howto-add-657-builtin-colours-to-the-flickr-dataset/)        