---
layout: post
title: "R and ggplot2: As per Cultural Analytics: Firefox Support Questions for an hour with x set to the minute the question was asked, logo plus 5 tokens from the question"
---
* Please refer to my previous post:  [R  and ggplot2: What if, as recommended by Cultural Analytics, I used the  actual text to make the graphic instead of converting the text to  numbers i.e. colours  ](http://rolandtanglao.com/2020/11/05/p1-use-the-actual-text-in-an-infographic-instead-of-converting-it-to-numbers/)        

* As per Cultural Analytics recommendations not to convert text to num,bers: Firefox Support Questions for an hour with x axis the minute, logo plus 5 tokens from the question See [sqlite-logo-text-hourly-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/sqlite-logo-text-hourly-ff-question-barcode.R)  and here is the code:

```r
#!/usr/bin/env Rscript
library(tidyverse)
library(DBI)
library(RSQLite)
library(rvest)
library(stopwords)
library(tokenizers)
library(ggimage)
library(lubridate)

set.seed(888)

getOSColour <- function(.x) {
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "black",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "gold",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "blue",
    TRUE ~ "purple"
  )
}

getLogo <- function(.x) {
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "LOGOS/macos-logo.png",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "LOGOS/linux-logo.png",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "LOGOS/windows-logo.png",
    TRUE ~ "LOGOS/purple-logo.png"
  )
}

getRandomQuestionText <- function(.x, .y) {
  # pick 5 random tokens
  tplusc <- paste(.x, html_text(read_html(.y)))
  print(tplusc)
  tplusc_tokens <-
    unlist(tokenize_words(tplusc, stopwords = stopwords::stopwords("en")))
  print(tplusc_tokens)
  token_length <- length(tplusc_tokens)
  num_tokens <- if (token_length >= 5) 5 else token_length
  
  index <- sort(sample(1:length(tplusc_tokens), num_tokens))
  print(index)
  
  tokenstring = paste(tplusc_tokens[index[1]],
                      tplusc_tokens[index[2]],
                      tplusc_tokens[index[3]],
                      tplusc_tokens[index[4]],
                      tplusc_tokens[index[5]])
  print(tokenstring)
  paste0("bold(\"", tokenstring, "\")")
}

initial.options <- commandArgs(trailingOnly = FALSE)
file.arg.name <- "--file="
script.name <-
  sub(file.arg.name, "", initial.options[grep(file.arg.name, initial.options)])
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
  cat("
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
    sprintf(
      "%4.4d-%2.2d-%2.2d-%4.4d-%2.2d-%2.2d-firefox-creator-answers-desktop-all-locales",
      year,
      month,
      day,
      year,
      month,
      day
    )
  db_filename <- sprintf("%s.db", base_name)
  date_str <- sprintf("%4.4d-%2.2d-%2.2d %2.2d", year, month, day, hour)
  
  ffquestionsdb <- dbConnect(RSQLite::SQLite(), db_filename)
  query_str <- sprintf(
    "select * from \"%s\" where (datetime(created) >= datetime(\"%s:00:00\") AND
    datetime(created) <= datetime(\"%s:59:59\"));",
    base_name,
    date_str,
    date_str
  )
  sqlitedf <- dbGetQuery(ffquestionsdb, query_str)
  reverse_df <- sqlitedf %>% map_df(rev)
  length = nrow(reverse_df)
  image_df <- reverse_df %>%
    mutate(x = minute(parse_date_time(created, "YmdhMSz"))) %>%
    mutate(icon = getLogo(tags)) %>% 
    mutate(y = seq.int(by = 5,
                        length = length,
                        from = 0)) %>% 
    mutate(os_colours  = map_chr(reverse_df$tags, getOSColour)) %>% 
    mutate(question =  map2_chr(reverse_df$title,
                                 reverse_df$content,
                                 getRandomQuestionText))       
  options(tibble.width = Inf)
  print(image_df)
  
  p <- ggplot(image_df, aes(x, y)) +
    geom_image(aes(image = icon)) + 
    geom_text(aes(label = question), colour = image_df$os_colours, 
              vjust = "inward", hjust = "inward", parse = TRUE, 
              nudge_y = 2.2, nudge_x = -8, size = 8) + 
    theme_void() + expand_limits(y = c(0, 60), x = c(0,60))

  png_filename <- sprintf("logo-text-hour-%2.2d-%s.png",
                          hour, base_name)

  ggsave(
    png_filename,
    p,
    width = 14.2222222222223,
    height = 14.2222222222223,
    dpi = 72,
    limitsize = FALSE
  ) # 14.2222222222223 = 1024/72dpi
  warnings()
}

sink("log.txt")
main()
sink()

```

### Output for October 20, 2020 2x12 AM on top, PM on bottom

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/50575257387/in/photolist-2k4aq1k-2k447zg-2k3ASoF-2k3AyPn" title="with formatting bugs mostly fixed! logo-text-20october2020-ff-questions-by-hour"><img src="https://live.staticflickr.com/65535/50575257387_f0c7036a25_b.jpg" width="1024" height="171" alt="with formatting bugs mostly fixed! logo-text-20october2020-ff-questions-by-hour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

### Next Steps

* Run this script for all of 2019 and 2020? To make some nice tshirts and tights from the graphics
* Add links? ggplot2 supports links in at least PDF. Might be a way to export to HTML too
* Change [geom_text() call](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/sqlite-logo-text-hourly-ff-question-barcode.R#L130) to use `scale_colour_manual()`?!? See [this stack overflow question](https://stackoverflow.com/questions/41541708/how-to-change-font-color-in-geom-text-in-ggplot2-in-r) for clues.

