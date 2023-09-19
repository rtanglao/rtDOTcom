---
layout: post
title: "How to create a 2 second fps video using ffmpeg  from lots of JPEGs e.g. from Canon EOS RP"
---
* How to create a 2 second fps video using ffmpeg (via [How to convert images using FFmpeg to create a simple slideshow](https://www.plainlyvideos.com/blog/ffmpeg-convert-images-to-video)]

```bash
ffmpeg -framerate 1/0.125 -pattern_type glob -i '*.JPG' \
-filter_complex "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2" \
-pix_fmt yuv420p -r 2 \
1frame-every-0.125seconds-2FPS-2023-09-02-concord-park-viaduct-dutch-taiwanfest-london-drugs-dunsmuir-revolver-bicycling.mp4
```
* Even better over 1.5 hours condensed into 26 seconds :-) !
```bash
ffmpeg -framerate 1/0.002 -pattern_type glob -i '*.JPG' -filter_complex "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2" -pix_fmt yuv420p -r 120 1frame-every-0.002seconds-120FPS-2023-09-04-eosrp-zeiss35mmf2-revolver-stanleypark-clarkpark-bicycling.mp4  
```

### Previously

* April 6, 2021: [Photoshop-less  way using printf and magick (imagemagick version 7) to convert an RGB  file created by xxd without a header to a PNG](http://rolandtanglao.com/2021/04/10/p1-photoshop-less-using-printf-header-magick-convert-xxd-rgb-png/)        

