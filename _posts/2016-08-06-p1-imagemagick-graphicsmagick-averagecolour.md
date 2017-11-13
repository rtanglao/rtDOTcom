---
layout: post
title: Dominant colour using imagemagick (and graphicsmagick) 
---
[Dominant colour using imagemagick](http://blog.endpoint.com/2011/04/determining-dominant-image-color.html) (and graphicsmagick: just add ```gm``` in front!)
```convert Waffle.jpg -scale 1x1\! -format '%[pixel:u]' info:-```
output:
```rgb(219,166,94)```