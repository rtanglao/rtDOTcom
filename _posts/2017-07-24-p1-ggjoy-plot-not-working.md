---
layout: post
title: "ggjoy() plot for instagram january 2016 average colour, average-colour-by-hour-ggjoy-from-csv.R,not working"
---

## Pontifications

* 1\. [average-colour-by-hour-ggjoy-from-csv.R not working](https://github.com/rtanglao/2016-r-rtgram/blob/master/average-colour-by-hour-ggjoy-from-csv.R)

```bash
Rscript ../average-colour-by-hour-ggjoy-from-csv.R 31-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv 
Error in FUN(X[[i]], ...) : need at least 2 data points
Calls: main ... <Anonymous> -> f -> <Anonymous> -> f -> vapply -> FUN
Execution halted
```

Here's the code:

```R
library(ggplot2)
library(plotrix)
library(plyr)
library(ggjoy)

tc <- function(x) {
  return (head(color.id(x), n = 1))
}

printf <- function(...) {
  invisible(print(sprintf(...)))
}

args <- commandArgs(TRUE)

## Default setting when no arguments passed
if (length(args) < 1) {
  args <- c("--help")
}
if ("--help" %in% args) {
  cat(
    "
    Arguments:
    CSV file with a column with colour with hex values for colours
    --help              - print this text
    Example:
    Rscript average-colour-by-hour-ggjoy-from-csv.R JANUARY2016/january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv\n\n"

  )
  q(save = "no")
}

main <- function() {
  data3 = read.csv(file = args[1], stringsAsFactors = F)
  data3$colourname <- sapply(data3$colour, tc)

  print(head(data3))

  p = ggplot(data3, aes(x = hour, y = colourname, stat= "identity")) +
      geom_joy()+
      ## geom_joy(scale = 3, rel_min_height = 0.01) +
      scale_y_discrete(expand = c(0.01, 0)) +   # will generally have to set the `expand` option
      ## scale_x_continuous(expand = c(0.01, 0)) +
      ## scale_y_discrete(expand = c(0.01, 0)) +
      labs(title = 'Average Colour',
           subtitle = 'Instagram 2016 Vancouver') +
      theme_joy(font_size = 13, grid = T) + theme(axis.title.y = element_blank())

  filename = sprintf("ggjoy-instagram-average-colour-%s", gsub("csv", "png", basename(args[1])))

  ggsave(filename,
         p,
         width = 14.222222222,
         height =10.666666667,
         dpi = 72,
         limitsize = FALSE) #multiply height and width by dpi to get px
  
}

sink("log.txt")

main()

sink()

```

* 2\.But I have two data points! namely for example the first 6 rows I have 3 rows with ```indianred4```

```
 colour                             id dayofweek.month.dayofmonth daynumber   unixtime  hour colourname
    <chr>                          <chr>                      <chr>     <int>      <int> <int>      <chr>
1 #546363 1174465369140103047_2176611536                   SunJan31        31 1454227203     0     gray37
2 #ACA8A8 1174465451560169285_2137478482                   SunJan31        31 1454227213     0   darkgray
3 #6B3434 1174465462824925338_2250967365                   SunJan31        31 1454227215     0 indianred4
4 #4B3E3E  1174465565628114803_177763144                   SunJan31        31 1454227227     0     gray26
5 #803A3A  1174465617924150379_361059564                   SunJan31        31 1454227233     0 indianred4
6 #704141 1174465676122308807_1537167607                   SunJan31        31 1454227240     0 indianred4
```