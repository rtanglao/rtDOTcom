---
layout: post
title: "Part 2 - mpg scatterplot - applied to average colour instagram by hour jan 1-31, 2016 - add colourname column"
---

## Pontifications

* [Part 1](http://rolandtanglao.com/2017/08/07/p1-mpg-scatterplot-average-colour-instagram-r-data-science/)
* I realized that adding the colourname on 100K rows is an expensive i.e. slow operation. Therefore instead of creating a visualization with the colournames in part 2, in part 2  I am really just going to create a CSV file with the colournames added as an additional column that I can reuse for many visualizations without having to repeat the expensive colourname lookup operation.
* Here's the relevant code from [https://github.com/rtanglao/2016-r-rtgram/blob/master/part2-create-csv-ig-van-average-colour-jan2016.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/part2-create-csv-ig-van-average-colour-jan2016.R): 

```R
tc <- function(x) {
  return (head(color.id(x), n = 1))
}
 csv_url = "https://raw.githubusercontent.com/rtanglao/2016-r-rtgram/master/JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv"
    average_colour_ig_van_jan2016 = read_csv(csv_url)
    print(average_colour_ig_van_jan2016)
    # the following line of code doesn't work because mutate just does the first value of the column
    # average_colour_ig_van_jan2016_with_colourname = mutate(average_colour_ig_van_jan2016, colourname = tc(colour))
   average_colour_ig_van_jan2016_with_colourname =  average_colour_ig_van_jan2016 %>% 
       rowwise() %>% 
       mutate(colourname = tc(colour))
    write_csv(average_colour_ig_van_jan2016_with_colourname,
              "january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour-colourname.csv")
```
* ```%>%``` is like the unix pipe operator
* ```rowwise()``` is required to repeat the function call on each row, without ```rowwise()``` you'll just repeat it row 1 repeatedly i.e. get the same value each time, the value of ```tc``` applied to the first row !
* ```mutate``` adds the ```colourname``` column by computing the colourname from the hexadecimal colour using the ```color.id``` function from the ```plotrix``` package
* This RScript was invoked as follows:

```bash
cd JANUARY2016
Rscript ../part2-create-csv-ig-van-average-colour-jan2016.R
```

* In [Part 3](http://rolandtanglao.com/2017/08/07/p3-part3-create-naive-scatterplot-with-colournames/), we'll create a visualization using the colour names.