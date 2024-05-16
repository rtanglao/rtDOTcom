---
layout: post
title: "feh --randomize is great for viewing random images; not great for making collages, use imagemagick instead"
---
* `feh` can't handle large numbers of thumbnails (and for some reason I never understood it said there were 5x thumbnails than there actually was) but it's great for small random collages.
* e.g. here's two
  * make a random collage with feh (imagemagick is probably faster!) `feh  --randomize -r . --montage --verbose -X -x -H 4000 -W 4000 -O  2024-05-08-random-montage.png -E 10 -y 10`
  * 10200 pixel by 10200 pixel command line which took 6 hours
    `feh -r . --montage  --verbose -X -x -H 10200 -W 10200 -O  reverse-filelist-borderless-10200x10200-2024-05-09-sort-mtime-montage.png -E 20 -y 20 -S mtime --conversion-timeout 1 --borderless --reverse -f  hopefully-just-png-jpg-files.txt`
* Here's my complete mastodon`feh` thread: [https://devdilettante.com/deck/@roland/112445889280926642](https://devdilettante.com/deck/@roland/112445889280926642)

## Previously

* October 29, 2022: [imagemagick  How To make a montage of images from average colour: 1st get average  colour by downsizing to 1x1 ; 2nd upscale with a fixed size; this  results in images in this case with 20x20 which at 80x24 leads to  1600x480](http://rolandtanglao.com/2022/10/29/p1-howto-imagemagick-montage-of-resized-1x1-average-colour/)        