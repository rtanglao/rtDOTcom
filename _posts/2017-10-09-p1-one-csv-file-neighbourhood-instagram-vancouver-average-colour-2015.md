---
layout: post
title: "One CSV File with instagram Vancouver 2015 neighborhood using lapply() to read the CSV file and then bind_rows() to combine the rows of the CSV files"
---

## Pontifications

* Using ```bind_rows()``` and ```lapply()```, I combined the [6 neighborhood CSV files](http://rolandtanglao.com/2017/10/08/p1-2015-instagram-vancouver-lat-long-to-neighbourhood-csv/) made with [add-neightbourhood-to-csv.rb](https://github.com/rtanglao/ig-ggmap/blob/7e8b30d967b61f8e10f75491f4427125b8605714/add-neightbourhood-to-csv.rb) for instagram vancouver 2015 into 1 file  called [ig\_van_2015-colour-lat-long-date-neighborhood.csv](https://github.com/rtanglao/ig-ggmap/blob/master/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/ig_van_2015-colour-lat-long-date-neighborhood.csv) using the following R code:

```R
# https://stackoverflow.com/questions/30242065/trying-to-merge-multiple-csv-files-in-r

ig_van_neighbourhood_2015 <- list.files(
  "/Users/rtanglao/Dropbox/GIT/ig-ggmap/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015", 
  pattern = "[[:print:]]*neighbourhood[[:print:]]*.csv",
  full.names = TRUE) %>% 
  lapply(read_csv) %>% 
  bind_rows
  
  write.csv(ig_van_neighbourhood_2015, 
          file = "ig_van_2015-colour-lat-long-date-neighborhood.csv",
          row.names=FALSE)
```