---

layout: post
title: "Imagemagick v7 is much faster than OilyPNG or VIPS for creating images, cropping them and montaging i.e. collaging them"
---

# Pontifications

* Forgot to mention 2 days ago in [How I made Art of Where Tights from Berlin photos](http://rolandtanglao.com/2020/02/17/p1-how-i-made-art-of-where-tights-berlin/)
* Imagemagick aka magick version 7 even on a "slow" ARM64 processor is much faster at cropping and montaging images (probably because it's in C/C++) than ruby solutions like VIPS and OilyPNG/ChunkyPNG. See [Did you catch the bug in yesterday's vips code? I've coded an oily_png version that is at least twice as fast!](http://rolandtanglao.com/2019/01/23/p1-did-you-get-catch-the-error-vips-code-yesterday-oilypng-twice-as-fast/)
* Extra bonus about using magick is that you don't have to write code. You just have to master its arcane syntax :-) which isn't that bad!
