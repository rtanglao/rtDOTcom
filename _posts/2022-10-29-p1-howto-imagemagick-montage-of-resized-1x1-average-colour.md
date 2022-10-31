---
layout: post
title: "imagemagick How To make a montage of images from average colour: 1st get average colour by downsizing to 1x1 ; 2nd upscale with a fixed size; this results in images in this case with 20x20 which at 80x24 leads to 1600x480"
---

* [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/) Oct 29, 2022 10:25  [How To make a montage of images from average colour: 1st get average colour by downsizing to 1x1 ; 2nd upscale with a fixed size; this results in images in this case with 20x20 which at 80x24 leads to 1600x480](https://legacy.imagemagick.org/discourse-server/viewtopic.php?t=24847)
```bash
magick montage '*.JPG[1x1]' -tile 80x24  -geometry '20x20+0+0' onestep.jpg
```
^^^^--- `Resize images after they have all been read in before montage overlays them onto its canvas. It also defines the size and the spacing between the tiles into which the images are drawn. If no size is specified the images will not be resized.` <-- which leads me to my current idea of doing this for 1920 random vancouver image every day! (80x24 is the VT100 size :-) <-- tweeted this: [HowTo Montage from avgcolour: 1)get avg colour by downsizing to 1x1 2)upscale w/fixed size eg 20x20 @ 80x24 = 1600x480
  `magick montage '/*.JPG[1x1]' -tile 80x24  -geometry '20x20+0+0' onestep.jpg` <-- idea: Do this for 1920 random vancouver images daily! (80x24 is VT100 size :-)](https://twitter.com/rtanglao/status/1586412750091472897)

### Previously

* September 2022: [Use Super Collider to make music from photo geodata and average colour?](http://rolandtanglao.com/2022/09/25/p1-super-collider-to-make-music-from-photo-geodata-and-average-colour/)        
* September 2021: [How  to create an ggrepel plot of R's 657 plotrix colours of the average  colour of my 2019-2020 flickr photos, x axis is time in unix seconds  since 1970 using R, y axis is the average colour using the plotrix  colours](http://rolandtanglao.com/2021/09/22/p1-howto-my-2019-2020-photos-x-unixtime-seconds-average-colour-657-plottrix-colours-ggrepel-ggplot-faceted-by-vancouver-year-month-date/)     
* April 2021: [How To Use Imagemagick Version 7 convert to to resize an image to get average colour](http://rolandtanglao.com/2021/04/03/p1-imagemagick-version-7-average-colour-using-convert/)        
* October 2017: [Maps of Vancouver Neighourhoods average colour over plotted](http://rolandtanglao.com/2017/10/12/p1-maps-of-vancouver-neighourhoods-average-colour-instagram/)        
