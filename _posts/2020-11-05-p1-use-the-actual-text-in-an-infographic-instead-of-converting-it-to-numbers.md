---
layout: post
title: "R and ggplot2: What if, as recommended by Cultural Analytics, I used the actual text to make the graphic instead of converting the text to numbers i.e. colours  "
---
* Please refer to my previous post:  [R  and ggplot2 barcode (pink: Windows, blue: macOS, green:Linux, purple:  unknown/other) of Firefox questions by hour arranged in a 2x12 collage  makes an interesting graphic, what if I did that for all of 2020? ](http://rolandtanglao.com/2020/10/27/p1-barcode-ggplot2-by-hour-concatenated-2by12/) and [Reading Notes - Cultural Analytics - Lev Manovich](http://rolandtanglao.com/2020/10/26/p1-cultural-analytics-lev-manovich-reading-notes/)        

* Instead of converting the text to a colour, I just tokenized it and picked 5 random tokens See [sqlite-text-hourly-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/sqlite-text-hourly-ff-question-barcode.R)  and here is the code:

```r
#!/usr/bin/env Rscript
library(tidyverse)
library(DBI)
library(RSQLite)
library(rvest)
library(stopwords)
library(tokenizers)
set.seed(888)

getOSColour <- function(.x) { 
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "blue",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "green",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "hotpink",
    TRUE ~ "purple")
}

getRandomQuestionText <- function(.x, .y) {
  # pick a random index between 1 and 80
  # and then get the next 79 characters of text from that index
  tplusc <- paste(.x, html_text(read_html(.y)))
  tplusc_tokens <- unlist(tokenize_words(tplusc, stopwords = stopwords::stopwords("en")))
  token_length <- length(tplusc_tokens)
  num_tokens <- if(token_length >= 5) 5 else token_length

  index <- sort(sample(1:length(tplusc_tokens), num_tokens))
  
  tokenstring = paste(
    tplusc_tokens[index[1]], tplusc_tokens[index[2]], 
    tplusc_tokens[index[3]], tplusc_tokens[index[4]], 
    tplusc_tokens[index[5]])
  paste0("bold(\"", tokenstring, "\")")
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
  base_name <- 
   sprintf("%4.4d-%2.2d-%2.2d-%4.4d-%2.2d-%2.2d-firefox-creator-answers-desktop-all-locales",
    year, month, day, year, month, day)
  db_filename <- sprintf("%s.db", base_name)
  date_str <- sprintf(
    "%4.4d-%2.2d-%2.2d %2.2d",year, month, day, hour)

  ffquestionsdb <- dbConnect(RSQLite::SQLite(), db_filename)  
  query_str <- sprintf(
    "select * from \"%s\" where (datetime(created) >= datetime(\"%s:00:00\") AND
    datetime(created) <= datetime(\"%s:59:59\"));",
    base_name, date_str, date_str
  )
  sqlitedf <- dbGetQuery(ffquestionsdb, query_str)
  reverse_df <- sqlitedf %>% map_df(rev)
  length = nrow(reverse_df)
  options(tibble.width = Inf)
  print(reverse_df)
  y <- seq.int(by = 5,length = length, from = 0)
  x <- integer(length)
  
  os_colours_vector <- map_chr(reverse_df$tags, getOSColour)
  question_text <- map2_chr(
    reverse_df$title,
    reverse_df$content, getRandomQuestionText)

  p <- ggplot() + theme_void()
  p <- p + annotate(
    "text", label = question_text, x = x, y=y, 
    color = os_colours_vector, parse = TRUE)
  png_filename <- sprintf(
    "text-hour-%2.2d-%s.png",
    hour, base_name)
  ggsave(png_filename, p, width = 3.555555556, height = 3.555555556, 
         dpi = 72, limitsize = FALSE) # 3.555555556 = 256/72dpi
  warnings()
}

sink("log.txt")
main()
sink()
```

### Output 

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/50568907451/in/photolist-2k3ASoF-2k3AyPn-2jZYPEU-2jZYxYK-2jZYxYu-2jZXNVe-2jZU6Er-2jZYxYe-2jZU6Eg-2jZYxXx-2jZYxXh-2jZXNU7-2jZU6DV-2jZXNTA-2jZXNTR-2jZYxVU-2jZU6D9-2jZU6Dj-2jZYxVJ-2jZU6Cc-2jZXNSo-2jZYxUr-2jZYxUg-2jZXNRM-2jZXNQp-2jZXNQ9-2jYaS4r-2jXRqcc-2juDA3H-2jhdvnH-2jhhAVH-2j7GJWV-2j7CH3o-2j7Fx5L-2j7BxYo-2ivrkMc-2ivoMB1-2iuuRHR-2itPBJA-2ifGD5o-2hFv3Gf-2jm8iaS-2jhftLc-2j9Qhia-2iAhjzA-2hRHaPU-2hR6M1b-2hEaCtg-2hxMftz-2hxQYub" title="with indexing bug fix! text-20october2020-ff-questions-by-hour"><img src="https://live.staticflickr.com/65535/50568907451_581f8513a5_b.jpg" width="1024" height="171" alt="with indexing bug fix! text-20october2020-ff-questions-by-hour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

### Next Steps

* Add logos for the operating systems i.e. a logo for macOS, Windows, Linux and other, should make it interesting
* Also perhaps change it so the x coordinate is a function of  the minute and second of the question in the hour? Instead of using the y coordinate which is what the current script does!