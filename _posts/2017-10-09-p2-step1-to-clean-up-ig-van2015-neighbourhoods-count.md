---
layout: post
title: "Step 1 of cleaning instagram vancouver 2015 neighbourhood dataset is to count the occurrences of each neighborhood using add_count() and filter()"
---

## Pontifications
(Step 2 is to remove those >100 occurrences whose neighborhoods aren't in the city of Vancouver, like North Vancouver, Whistler, Squamish, Burnaby, etc)

* Step 1 of [instagram vancouver 2015 neighbourhood data cleaning](http://rolandtanglao.com/2017/10/07/p1-2015-instagram-vancouver-lat-long-to-neighbourhood-flickr-api-done-next-remove-non-vancouver-hoods/): We'll derive [count\_ig_van\_2015-colour-lat-long-date-neighborhood.csv](https://github.com/rtanglao/ig-ggmap/blob/master/WITH_NEIGHBOURHOOD_CSV_FILES_FOR_GGMAP_2015/count_ig_van_2015-colour-lat-long-date-neighborhood.csv) as follows:
    * Using the data from the last post, [One CSV File with instagram Vancouver 2015 neighborhood using lappl(y) to read the CSV file and then bind_rows() to combine the rows of the CSV files](http://rolandtanglao.com/2017/10/09/p1-one-csv-file-neighbourhood-instagram-vancouver-average-colour-2015/), and ```add_count()``` and ```filter()``` we'll remove all rows whose neighborhood occurs less than 101 times using the following R code:

```R
count_ig_van_neighbourhood_2015  <-
  ig_van_neighbourhood_2015 %>% 
  add_count(neighbourhood, sort = TRUE) %>% 
  filter(n > 100)

write.csv(count_ig_van_neighbourhood_2015, 
          file = "count_ig_van_2015-colour-lat-long-date-neighborhood.csv",
          row.names=FALSE)
```