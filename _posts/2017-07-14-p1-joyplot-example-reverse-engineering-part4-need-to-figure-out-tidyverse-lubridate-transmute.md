---
layout: post
title: Reverse Engineering R joyplot code part 4 - Need to figure out what "%>%" really means and what tidyverse and transmute() do
---

## Pontifications

([Part 1](http://rolandtanglao.com/2017/07/10/p1-joyplot-r-reverse-engineering-part1/), [Part 2](http://rolandtanglao.com/2017/07/11/reverse-engineering-r-joyplot-code-part2-activity-tsv/), [Part 3](http://rolandtanglao.com/2017/07/13/p1-joyplot-example-reverse-engineering-part3-atusact-atussum/))

* From the [1\_gen\_data.R R Code](https://github.com/halhen/viz-pub/blob/master/sports-time-of-day/1_gen_data.R): 

```R
library(tidyverse)
library(lubridate)

# Load data; see https://www.kaggle.com/bls/american-time-use-survey

df.act <- read_csv('~henrik/private/vizyns/data/atus/atusact.csv')
df.sum <- read_csv('~henrik/private/vizyns/data/atus/atussum.csv')


# Get a data frame with activity (trcodep), observation weight (tufnwgtp)
# and interval for doing (start - end)

df.tmp <- df.act %>%
  filter(trtier2p == 1301) %>% # Doing sports/exercise
  
  # start and end are minutes since midnight
  transmute(tucaseid,
            trcodep,
            start = as.numeric(substring(tustarttim, 1, 2)) * 60 + as.numeric(substring(tustarttim, 4, 5)),
            end = as.numeric(substring(tustoptime, 1, 2)) * 60 + as.numeric(substring(tustoptime, 4, 5))) %>%
inner_join(df.sum %>% select(tucaseid, tufnwgtp)) %>%
```

* Hmmm I haven't dug into tidyverse and lubridate, time to dig into  these so I can figure out what the lines with ```%>%``` mean (other than some sort of data pipe?) and what ```transmute()``` does! I guess that will be in part 5!