---
layout: post
title: "How to create an encircled plot of R's 657 plotrix colours of the average colour of my 2019-2020 flickr photos, x axis is time in unix seconds since 1970 using ggalt and ggplot in R, y axis is the average colour using the plotrix colours"
---
* tl;dr running [theme-void-create-flickr-roland-2019-2020-average-colour-by-the-second-scale-free.R](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/theme-void-create-flickr-roland-2019-2020-average-colour-by-the-second-scale-free.R) creates [8000px-flickr-roland-2019-2020-average-colour-by-the-second-scale-free.png](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/OUTPUT_GRAPHICS/theme-void-8000px-flickr-roland-2019-2020-average-colour-by-the-second-scale-free.png)
* As well as being in dropbox, the datasets are also on on github:
    *  [2020-and-2019-roland-flickr-filename-integer-imavgcolour-plotrixavgcolour-metadata.csv](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/LARGE_CSV_FILES/2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-metadata.csv)
    *  dataset with unix time in seconds of data taken: [2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-unixtimedt.csv](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/LARGE_CSV_FILES/2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-unixtimedt.csv)
    *  These datasets are unwieldy since they are so large with lots of unneeded columns from the flickr API so the next post will be about smaller datasets that have just the data required.

## Previously

* [How  To: Parse Times from flickr and how to Use a specific timezone with R  and lubridate e.g. `America/Vancouver` (broken in lubridate 1.7.4 to  1.7.9)](http://rolandtanglao.com/2021/09/08/p1-howto-use-a-specific-timezone-lubridate-r/) 
* [ggplot2 ggalt geom_encircle() sample plot of average colour](http://rolandtanglao.com/2021/09/04/p1-ggalt-encircle/)        

## Code (since I don't trust github to last forever :-) 

```r
# generates
# https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/OUTPUT_GRAPHICS/flickr-roland-2019-2020-average-colour-by-the-second-scale-free.png

df_with_plotrix_colour  <- read_csv(
  "/Users/roland/Documents/GIT/files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-filename-integer-imavgcolour-plotrixavgcolour-metadata.csv")
df_with_plotrix_colour_unixtime_dt <- df_with_plotrix_colour  %>% 
  rowwise() %>% 
  mutate(unixtime_dt = 
           if_else(synth_75sqisvalid == 0, 0, as.numeric(parse_date_time(datetaken, "%Y-%m-%d %H:%M:%s"))))
write_csv(df_with_plotrix_colour_unixtime_dt,
          "/Users/roland/Documents/GIT/files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-filename-imavgcolour-plotrixavgcolour-unixtimedt.csv", na="")
pacific_df_with_plotrix_colour_unixtime_dt <-
  df_with_plotrix_colour_unixtime_dt %>%
  mutate(pacific_ymd = format(lubridate::with_tz(parse_date_time(datetaken, "%Y-%m-%d %H:%M:%s"),
                                                 "America/Vancouver"),"%Y-%m-%d"))
p4_colors_factor <- ggplot(pacific_df_with_plotrix_colour_unixtime_dt, aes(unixtime_dt,synth_plotrixcolour))
p4 <- p4_colors_factor + geom_encircle(aes(group=synth_plotrixcolour,
                                           colour=I(synth_plotrixcolour),
                                           fill=I(synth_plotrixcolour))) + 
  geom_point(aes(colour=I(synth_plotrixcolour)))  + facet_wrap(~ pacific_ymd, scales = "free") + theme_void()
```

## Output (flickr embed which might also break)



<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51470680553/in/datetaken-public/" title="theme-void-8000px-flickr-roland-2019-2020-average-colour-by-the-second-scale-free"><img src="https://live.staticflickr.com/65535/51470680553_eb229810ce.jpg" width="417" height="500" alt="theme-void-8000px-flickr-roland-2019-2020-average-colour-by-the-second-scale-free"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>