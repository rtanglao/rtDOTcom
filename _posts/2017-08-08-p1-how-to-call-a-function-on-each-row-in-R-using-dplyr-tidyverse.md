---
layout: post
title: "How to call a function on each row of a tibble  using the tidyverse and dplyr "
---

## Pontifications

* From [Applying a function to every row of a table using dplyr?](https://stackoverflow.com/questions/21818181/applying-a-function-to-every-row-of-a-table-using-dplyr/24728107#24728107):



<blockquote>
As of dplyr 0.2 (I think) rowwise() is implemented, so the answer to this problem becomes:
</blockquote>

* abstract code:

```R
tibble_to_apply_function_to %>% 
rowwise() %>% 
mutate(new_column = some_function(
some_column(s)_of_tibble_to_apply_function_to))
```

* real code from [https://github.com/rtanglao/2016-r-rtgram/blob/master/part2-create-csv-ig-van-average-colour-jan2016.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/part2-create-csv-ig-van-average-colour-jan2016.R) :

```R
average_colour_ig_van_jan2016_with_colourname =  
  average_colour_ig_van_jan2016 %>% 
    rowwise() %>% 
       mutate(colourname = tc(colour))
```

