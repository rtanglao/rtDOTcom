---
layout: post
title: "R and ggplot2 pseudo code for barcode of Firefox questions"
---
* (please refer to my previous post:  [What  infographics should I make from hourly FF support questions? Barcode  with a stripe for Operating System, and a stripe for hash of the  question?](http://rolandtanglao.com/2020/10/19/p1-hourly-infographics-from-firefox-questions/))

```r
p = ggplot() 

for (question in questions) {
  xintercept = xintercept + 0.15
  # set os_colour_of_bar to pink if windows, blue if macOS, green if linux, purple if unknown OS
  p = p + geom_vline(col=os_colour_of_bar, xintercept=xintercept)
  xintercept = xintercept + 0.15
 colour_of_bar = abs(digest::digest2int(question)) %% 657 # 657 colors in r
  p = p + geom_vline(col=colour_of_bar, xintercept = xintercept)
  # just keep incrementing the xintercept by 0.15 and changing colour_of_bar
}
```
