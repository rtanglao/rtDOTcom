---
layout: post
title: "R and ggplot2 barcode (pink: Windows, blue: macOS, green:Linux, purple: unknown/other) of Firefox questions by hour arranged in a 2x12 collage makes an interesting graphic, what if I did that for all of 2020? "
---
* Please refer to my previous post: [R and ggplot2 barcode of Firefox questions using no for loop - more optimizations, case...when, map2 and how it works](http://rolandtanglao.com/2020/10/23/p1-barcode-ggplot2-case-when-map2/)

* I took [no-for-loop-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/no-for-loop-ff-question-barcode.R) and made an hourly version that takes as an input the daily question file and the hour (0-23) and called it,  [hourly-ff-question-barcode.R]()  and here is the code:

```r
#!/usr/bin/env Rscript
library(tidyverse)
library(tibbletime)
library(lubridate)

colours_array <- colours()

getOSColour <- function(.x) { 
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "blue",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "green",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "hotpink",
    TRUE ~ "purple")
}

initial.options <- commandArgs(trailingOnly = FALSE)
file.arg.name <- "--file="
script.name <- sub(file.arg.name, "", initial.options[grep(file.arg.name, initial.options)])
script.basename <- dirname(script.name)

args <- commandArgs(TRUE)
year = as.integer(args[1])
month = as.integer(args[2])
day = as.integer(args[3])
hour = as.integer(args[4])

## Default setting when no arguments passed
if (length(args) < 4) {
  args <- c("--help")
} else {
  if (hour < 0 || hour > 23 || 
      year < 2010 || 
      month < 0 || month > 12) {
    args <- c("--help")
  }
}
                  
if ("--help" %in% args) {
  cat(
    "
    Arguments:
    year
    month
    day
    hour (0-23)
    --help              - print this text
    Example:")
    cat(paste("Rscript", script.name, "2020 10 20 23\n\n"))
  q(save = "no")
}
print(script.name)

main <- function() {
  filename <- sprintf(
  "%4.4d-%2.2d-%2.2d-%4.4d-%2.2d-%2.2d-firefox-creator-answers-desktop-all-locales.csv",
  year, month, day, year, month, day)

  csv <- read_csv(filename)
  # data frame needs to be in ascending order instead of descending
  reverse_csv <- csv %>% map_df(rev)
  csv_time <- reverse_csv %>%
    mutate(created_time = parse_date_time(created, orders = "ymdHMSz"))
  csv_tt <- as_tbl_time(csv_time, index = created_time)
  time_filter_str <- paste0(args[1], "-", args[2], "-", args[3], " ", args[4])
  hourly_csv <- csv_tt %>%
    filter_time(time_filter_str ~ time_filter_str)

  length <- nrow(hourly_csv)
  options(tibble.width = Inf)
  print(hourly_csv)
  xintercept <- seq.int(by = 10,
                        length = length * 2,
                        from = 0)
  size <- rep(c(4, 2), length = length * 2)
  os_colours_vector <- map_chr(hourly_csv$tags, getOSColour)
  question_colours_vector <- map2_chr(hourly_csv$title,
                                      hourly_csv$content,
                                      ~ {
                                        colours_array[(abs(digest::digest2int(paste(.x, .y))) %% 657) + 1]
                                      })
  colours_vector <-
    c(rbind(os_colours_vector, question_colours_vector))
  p <- ggplot() + theme_void()
  p <- p + geom_vline(col = colours_vector,
                      xintercept = xintercept,
                      size = size)
  png_filename <- sprintf(
    "hour-%2.2d-%4.4d-%2.2d-%2.2d-firefox-desktop-all-locales.png",
    hour, year, month, day, year, month, day)
  ggsave(png_filename, p, width = 3.555555556, height = 3.555555556, 
         dpi = 72, limitsize = FALSE) # 3.555555556 = 256/72dpi
  warnings()

}

sink("log.txt")
main()
sink()

```

* Then I ran it for all 24 hours of October 20, 2020 as follows:
```bash
for h in {0..23} do 
  Rscript ../hourly-ff-question-barcode.R 2020 10 20 $h 
done
```

* This produced these files (see [20october2020hour-files.txt](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/INFOGRAPHICS/20october2020hour-files.txt)):
```
hour-00-2020-10-20-firefox-desktop-all-locales.png
hour-01-2020-10-20-firefox-desktop-all-locales.png
hour-02-2020-10-20-firefox-desktop-all-locales.png
hour-03-2020-10-20-firefox-desktop-all-locales.png
hour-04-2020-10-20-firefox-desktop-all-locales.png
hour-05-2020-10-20-firefox-desktop-all-locales.png
hour-06-2020-10-20-firefox-desktop-all-locales.png
hour-07-2020-10-20-firefox-desktop-all-locales.png
hour-08-2020-10-20-firefox-desktop-all-locales.png
hour-09-2020-10-20-firefox-desktop-all-locales.png
hour-10-2020-10-20-firefox-desktop-all-locales.png
hour-11-2020-10-20-firefox-desktop-all-locales.png
hour-12-2020-10-20-firefox-desktop-all-locales.png
hour-13-2020-10-20-firefox-desktop-all-locales.png
hour-14-2020-10-20-firefox-desktop-all-locales.png
hour-15-2020-10-20-firefox-desktop-all-locales.png
hour-16-2020-10-20-firefox-desktop-all-locales.png
hour-17-2020-10-20-firefox-desktop-all-locales.png
hour-18-2020-10-20-firefox-desktop-all-locales.png
hour-19-2020-10-20-firefox-desktop-all-locales.png
hour-20-2020-10-20-firefox-desktop-all-locales.png
hour-21-2020-10-20-firefox-desktop-all-locales.png
hour-22-2020-10-20-firefox-desktop-all-locales.png
hour-23-2020-10-20-firefox-desktop-all-locales.png
```

* Which I then collaged/montaged into 2x12: row 1 is 0-12, row 2 is 13-23 as follows:

  ```bash
   magick montage -verbose -adjoin -tile 12x2 +frame +shadow +label -adjoin -geometry "256x256+0+0<" @20october2020hour-files.txt 20october2020-ff-questions-by-hour.png
  ```
  
* Which results in the following output:

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/50539241276/in/datetaken-public/" title="20october2020-ff-questions-by-hour"><img src="https://live.staticflickr.com/65535/50539241276_1564e80571_h.jpg" width="1600" height="267" alt="20october2020-ff-questions-by-hour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* This would make a super cool graphic for tshirts and what not if I ran it for all 365 days of 2020 right?

* Or even 2019?
