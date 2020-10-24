---
layout: post
title: "R and ggplot2 barcode of Firefox questions using no for loop - more optimizations, case...when, map2 and how it works"
---
* (please refer to my previous post: [R and ggplot2 barcode of Firefox questions using no for loop just map functions, gain is questionable :-) but worth it in the long run, learned lots from learn to purrr](http://rolandtanglao.com/2020/10/22/p1-barcode-ggplot2-no-for-loop/)

* More optimizations:
  *  i)  added ```case_when()``` which resulted in the deletion of 3 lines of code
  *  ii) used ```map2()``` which eliminated the lines of code that concatenate `title` and `content` and gets around the problem that a dataframe when passed to a map function is passed columnwise not rowwise
  
* How it works:

  * ```r
    #first bar is at 10, second is at 20, 3rd is at 30
    xintercept <- seq.int(by = 10, length = length * 2, from = 0) 
    ```
    
  * ```R
    # bars are alternately 4 wide and 2 wide
    size <- rep(c(4,2), length = length * 2) 
```

  * ```R
    # interleave os colour (blue, green, hotpink or purple) s with question colours
    # e.g. if q1 windows and q2 is mac then the vector is 
    c("hotpink", q1colour, "blue", q2colour)
    colours_vector <- c(rbind(os_colours_vector, question_colours_vector)) 
    ```
* Here's the actual code from [no-for-loop-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/no-for-loop-ff-question-barcode.R) with further optimizations:

```r
library(tidyverse)
colours_array <- colours()

getOSColour <- function(.x) { 
  case_when(
    str_detect(.x, "mac-os|os-x|osx|macos") ~ "blue",
    str_detect(.x, "linux|ubuntu|redhat|debian") ~ "green",
    str_detect(.x, "windows-7|windows-8|windows-10") ~ "hotpink"
    TRUE ~ "purple")
}

csv <- read.csv("https://raw.githubusercontent.com/rtanglao/rt-kits-api3/main/2020/2020-10-20-2020-10-20-firefox-creator-answers-desktop-all-locales.csv")
# see https://stackoverflow.com/questions/39975317/how-to-reverse-the-order-of-a-dataframe-in-r
reverse_csv <- csv %>% map_df(rev)
length <- nrow(reverse_csv)
xintercept <- seq.int(by = 10, length = length * 2, from = 0)
size <- rep(c(4,2), length = length * 2)
os_colours_vector <- map_chr(reverse_csv$tags, getOSColour)
question_colours_vector <- map2_chr(reverse_csv$title,
                                    reverse_csv$content,
  ~{colours_array[(abs(digest::digest2int(paste(.x, .y))) %% 657) + 1]})
colours_vector <- c(rbind(os_colours_vector, question_colours_vector))
p <- ggplot() + theme_void()
p <- p + geom_vline(col = colours_vector, 
                    xintercept = xintercept, size = size)
```