---
layout: post
title: "Users don't know when their antivirus breaks Firefox and it's not obvious to them so they don't mention it in their support requests"
---
# Pontifications

* The following plot  of AVG and Avast mentions in the first week of Firefox 58-65 (we know that in the first week of Firefox 65 that Avast broke Firefox and that several support questions were about Avast/Avg yet it's hardly mentioned more in 65 than other releases) release shows that users don't know when their antivirus breaks Firefox and it's not obvious to them so they don't mention it in their support requests:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/46333828794/in/dateposted-ff/" title="firefox58-65-mentions-of-avg-avast-week1-of-release"><img src="https://farm8.staticflickr.com/7884/46333828794_bd87a153b5.jpg" width="500" height="313" alt="firefox58-65-mentions-of-avg-avast-week1-of-release"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## Code:

```bash
cd ~/GIT/rt-kitsune-api/VISUALIZATIONS/WEEK1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 1 23 58 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 3 13 59 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 5 9 60 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 6 26 61 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 9 5 62 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 10 23 63 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2018 12 11 64 1
../../print-csv-ff-desktop-questions-id-content-created-product-tags-title-topic-firefoxversion-1releaseweek.rb 2019 1 29 65 1
mlr --csv cut -x -f  'product,topic,tags'  firefox*.csv > ff58-65-id-created-title-content-firefoxversion-1streleaseweek-day.csv
```

* and then run the r script in debug mode:

```r
commandArgs <- function(...) return(c("WEEK1/ff58-65-id-created-title-content-firefoxversion-1streleaseweek-day.csv", "no"))
debugSource("plot-avg-and-avast-mentions-1st-week.r")
rm(commandArgs)
```

* or from the bash command line run [plot-avg-and-avast-mentions-1st-week.r](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/plot-avg-and-avast-mentions-1st-week.r)

```bash
Rscript plot-avg-and-avast-mentions-1st-week.r WEEK1/ff58-65-id-created-title-content-firefoxversion-1streleaseweek-day.csv no
``` 
