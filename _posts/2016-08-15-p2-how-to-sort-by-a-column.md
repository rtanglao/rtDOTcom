---
layout: post
title: How to sort by a column using order() in R
---

Say you want to sort by some column in a datatable. Sample code below is from [colourname-void-square-piechart-from-csv.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/colourname-void-square-piechart-from-csv.R). Note the hilarious ```,]``` which makes me laugh whenever I encounter it. Not a disrespectful laugh but a this is not the "C/C++/ruby/python/php syntax" you are looking for laugh :-) !

```R
# "-" means descending sort order
samedatatable <- somedatatable[order(-somedatatable$name_of_count_field),]
# e.g. 
countcolourname <- countcolourname[order(-countcolourname$freq),]
# easy peasy right? as if :-)
# inch by inch
```
