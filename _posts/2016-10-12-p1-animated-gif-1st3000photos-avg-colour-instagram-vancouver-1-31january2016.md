---
layout: post
title: animated GIF of First 3000photos average colour instagram-vancouver 1-31January2016
---
## Pontifications

This animated GIF thing is fun, a fine way to repurpose and promote my instagram Vancouver visualizations :-) !

Full context see [my animated GIF git repo and scroll down to October 12, 2016](https://github.com/rtanglao/rt-animated-gifs):

* ```mkdir 2016-10-12```
* ```cd !$```
* ```convert -loop 50 -delay 20  @3000photos.txt 3000firstphotos-01-31January2016-avg-colour-per-hour.gif```
* OOOPS that makes an 1024x768 animated GIF we want 2:1 and maximum dimensions of 1024x512. Therefore, we use the ```-scale``` option to get that 2:1 ratio and get the height down to 512.
    * ```convert -loop 50 -delay 20  -scale 1024x512 @3000photos.txt 1024x512-scaled-3000firstphotos-01-31January2016-avg-colour-per-hour.gif```

### Output

![twitter size 01-31January2016-1st3000photos-avg-colour-per-hour](https://c2.staticflickr.com/8/7771/29661313004_98ffe1a6df_o_d.gif "twitter size 01-31January2016-1st3000photos-avg-colour-per-hour")