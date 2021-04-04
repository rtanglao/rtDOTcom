---
layout: post
title: "How To Use Imagemagick Version 7 convert to to resize an image to get average colour"
---
* `ggrep` because of OS X BSD  ridiculousness :-)
```bash
magick convert  2020-12-31-01-12-41-50781630447-IMG_4248.jpg \
-resize 1x1 txt:- | ggrep -Po "#[[:xdigit:]]{6}
#58473A
```
* Previously: 
  
    * From Imagemagick pre-version 7, February, 2017:[http://rolandtanglao.com/2017/02/21/p1-Average-colour-using-imagemagick-convert/](http://rolandtanglao.com/2017/02/21/p1-Average-colour-using-imagemagick-convert/)
    
```bash
convert rose: -scale 1x1 \
-format '%[fx:int(255*r+.5)],%[fx:int(255*g+.5)],%[fx:int(255*b+.5)]'\
info:-
```



