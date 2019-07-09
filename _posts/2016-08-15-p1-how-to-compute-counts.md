---
layout: post
title: How to compute counts using count() in R
---

Say you want to sum up how many times a colour appears in a data table in R? code from [computed-counts-first3-ig-van-01january2016-square-piechart.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/computed-counts-first3-ig-van-01january2016-square-piechart.R)

```R
some_data_table_withcounts = count(some_data_table, "column_to_count")
# e.g. 
countcolourname = count(data3, "colourname")
# easy peasy right? as if :-)
# inch by inch
```
