---
layout: post
title: "R and ggplot2 barcode of Firefox questions using no for loop just map functions, gain is questionable :-) but worth it in the long run, learned lots from learn to purrr"
---
* (please refer to my previous post: [R and ggplot2 barcode of Firefox questions using a for loop; functional version in next post](http://rolandtanglao.com/2020/10/21/p1-barcode-ggplot2-for-loop-kludge/))

* Was it worth it? Is code without `for` loops better?

* My answer is no, not for short programs but in the large probably! [I learned a lot from Rebecca Barter's Learn to purrr from 2018](http://www.rebeccabarter.com/blog/2019-08-19_purrr/) in the process! such as:

* 1\. The tilde-dot shorthand for functions will come handy in the future! Like ruby blocks, it is more compact to use this for simple functions instead having to write out a function and decide on a parameter name instead of just using `.x` 

```r
~{colours_array[(abs(digest::digest2int(.x)) %% 657) + 1]})
```
* 2\. map functions like `map_chr()` can't be passed in a whole data frame; they need to be passed a specific column.

* Here's the actual code from [no-for-loop-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/no-for-loop-ff-question-barcode.R) without the  "kludgy"  `for` loop:

```r
library(tidyverse)
colours_array <- colours()

getOSColour <- function(.x) { 
  os_colour <- "purple"
  macos_str <- "mac-os|os-x|osx|macos"
  windows_str <- "windows-7|windows-8|windows-10"
  linux_str <- "linux|ubuntu|redhat|debian"
  if(str_detect(.x, macos_str)) os_colour <- "blue"
  if(str_detect(.x, linux_str)) os_colour <- "green"
  if(str_detect(.x, windows_str)) os_colour <- "hotpink"
  return(os_colour)
}

csv <- read.csv("https://raw.githubusercontent.com/rtanglao/rt-kits-api3/main/2020/2020-10-20-2020-10-20-firefox-creator-answers-desktop-all-locales.csv")
# see https://stackoverflow.com/questions/39975317/how-to-reverse-the-order-of-a-dataframe-in-r
reverse_csv <- csv %>% map_df(rev)
length <- nrow(reverse_csv)
xintercept <- seq.int(by = 10, length = length * 2, from = 0)
size <- rep(c(4,2), length = length * 2)
reverse_csv_with_title_plus_content <- reverse_csv %>% 
  mutate(tplusc = paste(title, content))
os_colours_vector <- map_chr(reverse_csv$tags, getOSColour)
question_colours_vector <- map_chr(reverse_csv_with_title_plus_content$tplusc,
  ~{colours_array[(abs(digest::digest2int(.x)) %% 657) + 1]})
colours_vector <- c(rbind(os_colours_vector, question_colours_vector))
p <- ggplot() + theme_void()
p <- p + geom_vline(col = colours_vector, 
                    xintercept = xintercept, size = size)

```

## Output

Here's the [output](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/INFOGRAPHICS/3d1c382-no-for-loop-pink-windows-purple-other-blue-macos-green-linux-2020-10-20-2020-10-20-firefox-desktop-all-locales.png) (which is the same as the for loop output of course!)

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/50518762551/in/datetaken-public/" title="3d1c382-no-for-loop-pink-windows-purple-other-blue-macos-green-linux-2020-10-20-2020-10-20-firefox-desktop-all-locales"><img src="https://live.staticflickr.com/65535/50518762551_e0b0672ec0.jpg" width="500" height="450" alt="3d1c382-no-for-loop-pink-windows-purple-other-blue-macos-green-linux-2020-10-20-2020-10-20-firefox-desktop-all-locales"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>