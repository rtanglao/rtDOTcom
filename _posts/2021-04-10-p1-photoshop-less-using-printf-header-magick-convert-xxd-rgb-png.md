---
layout: post
title: "Photoshop-less way using printf and magick (imagemagick version 7) to convert an RGB file created by xxd without a header to a PNG"
---

* As per [Converting raw images without headers](https://stackoverflow.com/questions/62602215/converting-raw-images-without-headers) but in one step. No need to create an intermediate ppm file

```bash
{ printf "P6\n%d %d\n255\n" WIDTH HEIGHT ; cat YOURFILE; } > result.ppm
magick result.ppm result.png
{ printf "P6\n%d %d\n255\n" 222 222 ; \
cat no-filetype-2020-and-2019-roland-flickr-imagemagick-average-colours; } \
 | magick  - image88.png # <-- 1 step and therefore better :-)
# or in imagemagick version 6:
{ printf "P6\n%d %d\n255\n" 222 222 ; \
cat no-filetype-2020-and-2019-roland-flickr-imagemagick-average-colours; } \
 | convert  - image88.png
```
* See previous post on how to do this with `ffmpeg`: [Photoshop-less way using ffmpeg to convert an RGB file created by xxd without a header to a PNG](http://rolandtanglao.com/2021/04/06/p1-ffmpeg-photoshop-convert-raw-rgb-file-without-headers-to-png/)

