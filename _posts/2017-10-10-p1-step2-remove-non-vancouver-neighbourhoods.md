---
layout: post
title: "Step 2 - Remove non Vancouver Neighbourhoods using tidyverse filter()"
---

## Pontifications
([Step 1 of cleaning instagram vancouver 2015 neighbourhood dataset is to count the occurrences of each neighborhood using add_count() and filter()](http://rolandtanglao.com/2017/10/09/p2-step1-to-clean-up-ig-van2015-neighbourhoods-count/))

```R
filter_step2_ig_van_neighbourhood_2015  <-
  ig_van_neighbourhood_2015 %>% 
  filter(neighbourhood != "Maywood") %>% 
  filter(neighbourhood != "Whistler") %>%
  filter(neighbourhood != "Burnaby") %>%
  filter(neighbourhood != "Vancouver") %>%
  filter(neighbourhood != "North Vancouver") %>%
  filter(neighbourhood != "Surrey" ) %>%
  filter(neighbourhood != "Norgate" ) %>%
  filter(neighbourhood != "Deep Cove" ) %>%
  filter(neighbourhood != "Sea Island" ) %>%
  filter(neighbourhood != "Stride Hill" ) %>%
  filter(neighbourhood != "West Vancouver" ) %>%
  filter(neighbourhood != "Keith-Lynn" ) %>%
  filter(neighbourhood != "Laurentian Belaire" ) %>%
  filter(neighbourhood != "Greater Vancouver" ) %>%
  filter(neighbourhood != "Cleveland Park" ) %>%
  filter(neighbourhood != "Capilano" ) %>%
  filter(neighbourhood != "Park Royal" ) %>%
  filter(neighbourhood != "Ubc" ) %>%
  filter(neighbourhood != "Squamish-Lillooet" ) %>%
  filter(neighbourhood != "Horseshoe Bay" ) %>%
  filter(neighbourhood != "Golden Village" )
```