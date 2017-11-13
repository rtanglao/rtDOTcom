---
layout: post
title: "R - Group_by() and tally() error message: Grouping rowwise data frame strips rowwise nature "
---

## Pontifications

```R
sept072017_colourname_n <- 
  sept042017_int_colour_ig_van_june2016_average_colour %>% 
+roup_by(colourname ) %>% 
+tally()
```

Error message:
```
Using `n` as weighting variable
Warning message:
Grouping rowwise data frame strips rowwise nature 
```

* Why? The result is fine!

```
> sept072017_colourname_n
# A tibble: 173 x 2
    colourname    nn
         <chr> <int>
 1 aquamarine3  2043
 2 aquamarine4 19617
 3      azure2   100
 4      azure3  3114
 5      azure4 35912
 6     bisque3   706
 7     bisque4 11893
 8       black    36
 9       brown  6392
10      brown3   725
# ... with 163 more rows
```