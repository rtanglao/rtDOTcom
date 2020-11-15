---
layout: post
title: "R and ggplot2: ggrepel positions labels so they do not overlap"
---
* Please refer to my previous post:  [R and ggplot2: How to set literal colour values: use the 'as is' function aka I() instead of scale_colour_identity()](http://rolandtanglao.com/2020/11/11/p1-ggplot2-set-literal-colour_values_with_scale_colour_identity/)       

* The `ggrepel` package positions labels so they don't overlap and it's great! Thanks!

* See the output and source code below

## Output

Output for October 20, 2020 hourly arranged 2x12 AM on top, PM on bottom:

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/50595229663/in/album-72157716861637001/" title="with ggrepel logo-text-20october2020-ff-questions-by-hour"><img src="https://live.staticflickr.com/65535/50595229663_61c2a73fdb_b.jpg" width="1024" height="171" alt="with ggrepel logo-text-20october2020-ff-questions-by-hour"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>


## Source

From [sqlite-logo-text-hourly-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/sqlite-logo-text-hourly-ff-question-barcode.R)

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
library(ggrepel)

set.seed(888)

get_os_colour <- function(.x) {
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "black",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "gold",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "blue",
    TRUE ~ "purple"
  )
}

get_logo <- function(.x) {
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "LOGOS/macos-logo.png",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "LOGOS/linux-logo.png",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "LOGOS/windows-logo.png",
    TRUE ~ "LOGOS/purple-logo.png"
  )
}

get_random_question_text <- function(.x, .y) {
  # pick 5 random tokens
  tplusc <- paste(.x, html_text(read_html(.y)))
  print(tplusc)
  tplusc_tokens <-
    unlist(tokenize_words(tplusc, stopwords = stopwords::stopwords("en")))
  print(tplusc_tokens)
  token_length <- length(tplusc_tokens)
  num_tokens <- if (token_length >= 5) 5 else token_length
  index <- sort(sample(seq_len(length(tplusc_tokens)), num_tokens))
  print(index)
  tokenstring <- paste(tplusc_tokens[index[1]],
                      tplusc_tokens[index[2]],
                      tplusc_tokens[index[3]],
                      tplusc_tokens[index[4]],
                      tplusc_tokens[index[5]])
  print(tokenstring)
  paste0("bold(\"", tokenstring, "\")")
}

initial_options <- commandArgs(trailingOnly = FALSE)
file_arg_name <- "--file="
script_name <-
  sub(file_arg_name, "", initial_options[grep(file_arg_name, initial_options)])
script_base <- dirname(script_name)
args <- commandArgs(TRUE)
year <- as.integer(args[1])
month <- as.integer(args[2])
day <- as.integer(args[3])
hour <- as.integer(args[4])

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
  cat(paste("Rscript", script_name, "2020 10 20 23\n\n"))
  q(save = "no")
}
print(script_name)

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
  reverse_df <- sqlitedf %>%
    map_df(rev)
  length <- nrow(reverse_df)
  image_df <- reverse_df %>%
    mutate(x = minute(parse_date_time(created, "YmdhMSz"))) %>%
    mutate(icon = get_logo(tags)) %>%
    mutate(y = seq.int(
      by = 5, length = length, from = 0)) %>%
    mutate(os_colours  = map_chr(reverse_df$tags, get_os_colour)) %>%
    mutate(question =  map2_chr(reverse_df$title,
                                 reverse_df$content,
                                 get_random_question_text))
  options(tibble.width = Inf)
  print(image_df)
  p <- ggplot(image_df, aes(x, y)) +
    geom_image(aes(image = icon)) +
    geom_label_repel(aes(label = question, colour = I(os_colours)),
              vjust = "inward", hjust = "inward", parse = TRUE,
              nudge_y = 2.5, nudge_x = -8, size = 3) +
    theme_void() + expand_limits(y = c(0, 60), x = c(0, 60))
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



