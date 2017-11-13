---
layout: post
title: Using sapply() to get colour as colour names aka calling a function on a column and adding the result as a new column to data table
---

```R
some-datatable$newcolumn <-
sapply(some-datatable$oldcolumn,
function-to-be-called-on-each-member-of-the-column)
```

from [colourname-void-piechart-from-CSV.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/colourname-void-piechart-from-csv.R):

```R
# function to be called on each element of the colour column
tc <-
     function(x) {
         return (head(color.id(x),n=1))
     }
...
data3$colourname <- sapply(data3$colour, tc)
# easy peasy right?
```
