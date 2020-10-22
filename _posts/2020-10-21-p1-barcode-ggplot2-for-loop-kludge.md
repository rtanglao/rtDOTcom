---
layout: post
title: "R and ggplot2 barcode of Firefox questions using a for loop; functional version in next post"
---
* (please refer to my previous post:  [R and ggplot2 pseudo code for barcode of Firefox questions](http://rolandtanglao.com/2020/10/20/p1-barcode-ggplot2-kludge/))
* Here's the actual code from [simplest-possible-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/simplest-possible-ff-question-barcode.R) with a kludgy `for` loop (I think it will be better without a `for` loop using a more functional style, but that will have to wait for the next post :-) !):

```r
library(tidyverse)
csv <- read.csv("https://raw.githubusercontent.com/rtanglao/rt-kits-api3/main/2020/2020-10-20-2020-10-20-firefox-creator-answers-desktop-all-locales.csv")
xintercept <- -10.0

# see https://stackoverflow.com/questions/39975317/how-to-reverse-the-order-of-a-dataframe-in-r
reverse_csv <- csv %>% map_df(rev)

p <- ggplot() + theme_void()
macos_str <- "mac-os|os-x|osx|macos"
windows_str <- "windows-7|windows-8|windows-10"
linux_str <- "linux|ubuntu|redhat|debian"
colours_array <- colours()

for (row in 1:nrow(reverse_csv)) {
  tags <- reverse_csv[row, "tags"]
  title_plus_content  <- paste(
    reverse_csv[row, "title"],
    reverse_csv[row, "content"])

  print(paste("Title:", title_plus_content, 
                " tags:", tags))
  xintercept <- xintercept + 10.0
  # set os_colour_of_bar to pink if windows, blue if macOS, green if linux, purple if unknown OS
  os_colour_bar <- "purple"
  if(str_detect(tags, macos_str)) os_colour_bar <- "blue"
  if(str_detect(tags, linux_str)) os_colour_bar <- "green"
  if(str_detect(tags, windows_str)) os_colour_bar <- "hotpink"
    
  p <- p + geom_vline(col=os_colour_bar, xintercept=xintercept, size=4)
  xintercept <- xintercept + 10.0
  colour_of_bar <- abs(digest::digest2int(title_plus_content)) %% 657 # 657 colors in r
  p <- p + geom_vline(col=colours_array[colour_of_bar + 1], 
                     xintercept = xintercept, size = 2)
}
```

## Output

Here's the [output](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/INFOGRAPHICS/4691ea0-pink-windows-purple-other-blue-macos-green-linux-2020-10-20-2020-10-20-firefox-desktop-all-locales.png):

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/50515163521/in/datetaken-public/" title="4691ea0-pink-windows-purple-other-blue-macos-green-linux-2020-10-20-2020-10-20-firefox-desktop-all-locales"><img src="https://live.staticflickr.com/65535/50515163521_07cb951a82.jpg" width="500" height="358" alt="4691ea0-pink-windows-purple-other-blue-macos-green-linux-2020-10-20-2020-10-20-firefox-desktop-all-locales"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>