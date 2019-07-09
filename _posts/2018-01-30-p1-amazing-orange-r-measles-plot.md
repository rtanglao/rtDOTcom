---
layout: post
title: "Amazing orange measles plot using r, ggpplot"
---

## Pontifications

Amazing orange measles plot using r, ggpplot using a red colour palette (hence the orange) in [Some datasets for teaching data science](https://simplystatistics.org/2018/01/22/the-dslabs-package-provides-datasets-for-teaching-data-science/)

**QUOTE**

<blockquote>

Contagious disease data for US states<br /><br />

This dataset contains yearly counts for Hepatitis A, measles, mumps, pertussis, polio, rubella, and smallpox for US states. Original data courtesy of Tycho Project. I use it to show ways one can plot more than 2 dimensions.

</blockquote>

**END QUOTE**

```r
library(RColorBrewer)
data("us_contagious_diseases")
the_disease <- "Measles"
us_contagious_diseases %>%
  filter(!state%in%c("Hawaii","Alaska") & disease ==  the_disease) %>%
  mutate(rate = count / population * 10000 * 52 / weeks_reporting) %>%
  mutate(state = reorder(state, rate)) %>%
  ggplot(aes(year, state,  fill = rate)) +
  geom_tile(color = "grey50") +
  scale_x_continuous(expand=c(0,0)) +
  scale_fill_gradientn(colors = brewer.pal(9, "Reds"), trans = "sqrt") +
  geom_vline(xintercept=1963, col = "blue") +
  theme_minimal() +  theme(panel.grid = element_blank()) +
  ggtitle(the_disease) +
  ylab("") +
  xlab("")
```

* Much to learn from the above code!