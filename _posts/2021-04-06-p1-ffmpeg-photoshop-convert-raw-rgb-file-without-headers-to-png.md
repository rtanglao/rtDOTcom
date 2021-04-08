---
layout: post
title: "Photoshop-less way using ffmpeg to convert an RGB file created by xxd without a header to a PNG"
---

* As per [Convert raw RGB32 file to JPEG or PNG using FFmpeg](https://stackoverflow.com/questions/46310408/convert-raw-rgb32-file-to-jpeg-or-png-using-ffmpeg), here's how to convert a  `.raw` file of RGB values without a header to a PNG

```bash
xxd -l 49284 -u -r -p \
2020-and-2019-roland-flickr-imagemagick-average-colours.txt\
2020-and-2019-roland-flickr-imagemagick-average-colours.raw
ffmpeg -f rawvideo -pixel_format rgb24 -video_size 222x222 \
-i 2020-and-2019-roland-flickr-imagemagick-average-colours.raw \
-frames:v 1 output.png
 mv output.png ffmpeg-2020-and-2019-roland-flick-average-colour-output.png
```
* Untested but perhaps adding a header like the following will work (as per [Converting raw images without headers](https://stackoverflow.com/questions/62602215/converting-raw-images-without-headers) (and then convert the ppm file to PNG using `imagemagick`)?
```bash
{ printf "P6\n%d %d\n255\n" WIDTH HEIGHT ; cat YOURFILE; } > result.ppm
```
* See [Average colour according to imagemagick resize of my flickr photos Jan 1, 2019 - Dec 31, 2020](http://rolandtanglao.com/2021/04/05/p1-rename-file-from-rgb-to-raw-opened-photoshop-converted-to-png/) where I document how to do it  with Photoshop and the `xxd` command to get the raw file

