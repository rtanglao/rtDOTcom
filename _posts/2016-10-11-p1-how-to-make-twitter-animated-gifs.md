---
layout: post
title: How to make twitter animated GIFs (1024x512)
---
## Pontifications

* [As of this writing, according to the Always Up-To-Date Social Media Image Sizes Cheat Sheet, twitter can only handle 1024x512 and 2:1 GIFs](https://docs.google.com/spreadsheets/d/1IpTYTTMJLcSXcPDtW9zSbPBHQyRdrLfKERohGIIkE_Q/edit#gid=0)
* So since twitter can't handle 1023x683 gifs from my instagram infographics and it can only handle 1024x512 wide therefore use ```-scale 1024x512``` ([full context over on github, scroll down to October 11, 2016](https://github.com/rtanglao/rt-animated-gifs)):
    * ```convert -loop 50 -delay 20 -scale 1024x512 @1-31jan2016pngs.txt 1024x512-imagemagick-01-31January2016-24squares-avgç-colour-per-hour.gif```

### Output

![twitter size 01-31January2016-24squares-avg-colour-per-hour](https://c2.staticflickr.com/6/5550/29638597234_dbb748ff10_o_d.gif "twitter size 01-31January2016-24squares-avg-colour-per-hour")