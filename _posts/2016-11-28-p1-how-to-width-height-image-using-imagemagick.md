---
layout: post
title: How To -- Get the width and height of an image using imagemagick
---

## Pontifications

* ```gm identify -format "%w %h\n" 0000001-flickr-roland-2004-12-avgcolour.png ``` or if you only have imagemagick then:
* ```identify -format "%w %h\n" 0000001-flickr-roland-2004-12-avgcolour.png ```
* some of the documentation implies that you can format it like printf using something like ```%03w``` to force zero padding with 3 zeroes but I couldn't get it to work (i tried using imagemagick 6.9, maybe it's fixed in 7):
    * [https://www.imagemagick.org/Usage/files/](https://www.imagemagick.org/Usage/files/)
    * [http://www.imagemagick.org/Usage/files/#save_escapes](http://www.imagemagick.org/Usage/files/#save_escapes)