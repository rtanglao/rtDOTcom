---
layout: post
title: Reverse Engineering R joyplot code part 2 -1_gen_data.R generates the activity.tsv file 
---

## Pontifications

([Part 1](http://rolandtanglao.com/2017/07/10/p1-joyplot-r-reverse-engineering-part1/))

* Maybe I should believe this comment :-) ```1_gen_data.R generates the activity.tsv file that is used in here```
* Looking at [1\_gen\_data.R](https://github.com/halhen/viz-pub/blob/master/sports-time-of-day/1_gen_data.R):

```R
library(tidyverse)
library(lubridate)

# Load data; see https://www.kaggle.com/bls/american-time-use-survey

df.act <- read_csv('~henrik/private/vizyns/data/atus/atusact.csv')
df.sum <- read_csv('~henrik/private/vizyns/data/atus/atussum.csv')


# Get a data frame with activity (trcodep), observation weight (tufnwgtp)
# and interval for doing (start - end)
```

* Therefore I guess it's time to look at [https://www.kaggle.com/bls/american-time-use-survey](https://www.kaggle.com/bls/american-time-use-survey) That will be part 3 :-) ! 