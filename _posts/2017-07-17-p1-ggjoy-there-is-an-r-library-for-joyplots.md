---
layout: post
title: "There's an R library for that: ggjoy for joyplots YES AND THANK-YOU!!"
---

## Pontifications

* Following up on [Reverse Engineering R joyplot code part 4 - Need to figure out what "%>%" really means and what tidyverse and transmute() do](http://rolandtanglao.com/2017/07/14/p1-joyplot-example-reverse-engineering-part4-need-to-figure-out-tidyverse-lubridate-transmute/), why bother reverse engineering when there's an R library for joyplots called ```ggjoy```?!?
* I kid, I think I will still try reverse engineering that code
* In the meantime feast on this awesomeness:

From [The joy of no more violin plots](https://simplystatistics.org/2017/07/13/the-joy-of-no-more-violin-plots/):

```R
library(ggjoy)
dat %>% mutate(group = reorder(group, value, median)) %>%
  ggplot(aes(x=value, y=group, height=..density..)) +
  geom_joy(scale=0.85)
```
  