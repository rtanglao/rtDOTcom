---
layout: post
title: "How to create a smaller dataset with just a flag to indicate whether average colour is present, plotrix average colour, date taken in unix time, yyyy-mm-dd "
---
* 1\. write a CSV file with pacific time zone yyyy-mm-dd
```r
write_csv(pacific_df_with_plotrix_colour_unixtime_dt,
"/Users/roland/Documents/GIT/rt-flickr-sqlite-csv/LARGE_CSV_FILES/pacific-yyyy-mm-dd-2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-unixtimedt.csv",
na="")
```
* 2\. write a CSV file with only the columns we need
```bash
mlr --csv cut -f datetaken,synth_plotrixcolour,synth_75sqisvalid,pacific_ymd \                      
pacific-yyyy-mm-dd-2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-unixtimedt.csv |\
grep -v "UTC,0," > pacific-yyyy-mm-dd-2020-2019-roland-flickr-datetaken-synth_75sqisvalid-synth_plotrixcolour.csv
```
* 3\. ooops forgot unixtime_dt
```bash
mlr --csv cut -f datetaken,synth_plotrixcolour,synth_75sqisvalid,unixtime_dt,pacific_ymd\                      
 pacific-yyyy-mm-dd-2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-unixtimedt.csv |\
grep -v "UTC,0," > pacific-yyyy-mm-dd-2020-2019-roland-flickr-datetaken-synth_75sqisvalid-synth_plotrixcolour_unixtimedt.csv
```
* This smaller dataset is  on on github:
    *  [rt-flickr-sqlite-csv/main/LARGE_CSV_FILES/pacific-yyyy-mm-dd-2020-2019-roland-flickr-datetaken-synth_75sqisvalid-synth_plotrixcolour_unixtimedt.csv](https://media.githubusercontent.com/media/rtanglao/rt-flickr-sqlite-csv/main/LARGE_CSV_FILES/pacific-yyyy-mm-dd-2020-2019-roland-flickr-datetaken-synth_75sqisvalid-synth_plotrixcolour_unixtimedt.csv)

## Previously

* [How  to create an encircled plot of R's 657 plotrix colours of the average  colour of my 2019-2020 flickr photos, x axis is time in unix seconds  since 1970 using ggalt and ggplot in R, y axis is the average colour  using the plotrix colours](http://rolandtanglao.com/2021/09/14/p1-howto-my-2019-2020-photos-x-unixtime-seconds-average-colour-657-plottrix-colours-encircled-ggalt-ggplot-faceted-by-vancouver-year-month-date/)        