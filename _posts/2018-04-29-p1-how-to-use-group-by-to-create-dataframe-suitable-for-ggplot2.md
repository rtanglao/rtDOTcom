---
layout: post
title: "How to use group_by to create a data frame in R suitable for ggplot2 and tidyverse"
---

## Pontifications

* use ```group_by()``` and ```count()``` as in:

```R
one_two_star_day <-
  one_and_two_star_with_date %>%
  group_by(date_updated) %>%
   count()
```
### Full code 

```R
library(tidyverse)
reviews = read.csv("20april2018-01nov2017-18april2018-mongo-export-reviews.csv")
one_and_two_star_reviews = reviews %>%
filter(star_rating < 3)
one_and_two_star_with_date <- one_and_two_star_reviews %>%
mutate(date_updated = as.Date(review_last_updated_time))

one_two_star_day <-
  one_and_two_star_with_date %>%
  group_by(date_updated) %>%
   count()

p = ggplot(
  data =one_two_star_day,
           aes(x=date_updated, y=n)) +
  geom_line(stat = "identity")+
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  scale_fill_brewer(palette = "Set1")
```

### Output 

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/41795849951/in/dateposted-public/" title="line chart of 1 and 2 star reviews nov 1, 2017  - april 18, 2018"><img src="https://farm1.staticflickr.com/977/41795849951_af5a0c8d6e_n.jpg" width="320" height="213" alt="line chart of 1 and 2 star reviews nov 1, 2017  - april 18, 2018"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>



