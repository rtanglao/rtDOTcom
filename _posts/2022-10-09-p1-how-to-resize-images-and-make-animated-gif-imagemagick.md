---
layout: post
title: "How to resize images to Twitter animated GIF dimensions and then make an animated GIF using imagemagick"
---
* [Discovered](http://rolandtanglao.com/2022/09/25/p1-super-collider-to-make-music-from-photo-geodata-and-average-colour/) Oct 6, 2022. 17:58  [magick commands  in linux on WSL to make an animated GIF](https://twitter.com/rtanglao/status/1578187282540277761):
```bash
parallel ~/bin/magick convert {}  -resize 1200x675  small-{/.}.jpg \
:::  /mnt/c/Users/rolan/OneDrive/Pictures/BEES_04OCT_2022/*.JPG
~/bin/magick convert -delay 20 -loop 0 `ls -1 *.jpg` 04oct2022beeflying.gif
```
* `imagemagick` version 7 is accessed via the `magick` commands. Version 6 is accessed via `convert` directly.
* There's probably a way to do this in 1 step using reading from stdin but I couldn't figure it out :-)

### Previously 
* August 2021: [How  To install Imagemagick on Ubuntu 20.04 with JPG, PNG and TIFF support  aka 'delegates'? Why isn't this in the default install?](http://rolandtanglao.com/2021/04/26/p1-how-to-install-imagemagick-ubuntu-2004-jpeg-png-tiff-delegates/)
* April 2021: [Not  an imagemagick bug but an unclean data problem: one of the rows is  missing an average colour because there was no thumbnail in flickr](http://rolandtanglao.com/2021/04/12/p1-data-not-clean-problem-not-imagemagick-bug/)
* April 2021:  [Photoshop-less  way using printf and magick (imagemagick version 7) to convert an RGB  file created by xxd without a header to a PNG](http://rolandtanglao.com/2021/04/10/p1-photoshop-less-using-printf-header-magick-convert-xxd-rgb-png/)
* April 2021: [Average colour according to imagemagick resize of my flickr photos Jan 1, 2019 - Dec 31, 2020](http://rolandtanglao.com/2021/04/05/p1-rename-file-from-rgb-to-raw-opened-photoshop-converted-to-png/)
* April 2021: [How To Use Imagemagick Version 7 convert to to resize an image to get average colour](http://rolandtanglao.com/2021/04/03/p1-imagemagick-version-7-average-colour-using-convert/) 
* February 2020: [Imagemagick v7 is much faster than OilyPNG or VIPS for creating images, cropping them and montaging i.e. collaging them](http://rolandtanglao.com/2020/02/19/p1-magick-is-faster-than-vips-or-ruby-oilypng-chunkypng/)
* August 2019: [HowTo: Circular Crop with ImageMagick](http://rolandtanglao.com/2019/08/15/p1-how-to-use-imagemagick-circular-crop/)        
