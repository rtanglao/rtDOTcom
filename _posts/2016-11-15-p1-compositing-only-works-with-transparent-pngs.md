---
layout: post
title: ImageMagick Compositing only works with transparent PNGs
---

tl;dr if the PNGs are not transparent then you can't overlay / composite!

## Pontifications

* [Generate Transparent GIF files in R using ```bg = "transparent"```:](https://github.com/rtanglao/rt-animated-gifs/commit/02cf7f14db59de2ee75b2d0748bca734b5af7d15) (I learned this from [a stack overflow question on ggplot2 transparency](http://stackoverflow.com/questions/7455046/how-to-make-graphics-with-transparent-background-in-r-using-ggplot2); [official png() docs](https://stat.ethz.ch/R-manual/R-devel/library/grDevices/html/png.html))<br /> ```png(file=filename, width=1024, height=1024, res=72, bg = "transparent")```
* Then everything works:

```sh
convert 0000001-first360-flickr-roland-2004-12-avgcolour.png 0000002-first360-flickr-roland-2004-12-avgcolour.png\ 
-composite 1-2.png
convert 1-2.png 0000003-first360-flickr-roland-2004-12-avgcolour.png\ 
-composite 1-2-3.png
convert 1-2-3.png 0000004-first360-flickr-roland-2004-12-avgcolour.png\ 
-composite 1-2-3-4.png
convert 1-2-3-4.png 0000005-first360-flickr-roland-2004-12-avgcolour.png\ 
-composite 1-2-3-4-5.png
```