---

layout: post
title: "Zazzle infographic from Berlin July 2019 - 75 pixel circular thumbnail from 168 thumbnails (24x28 = 1800px2100px) (spot yesterday's bug: 'ls -1tr' instead of 'ls -1')"
---

# Pontifications

* Did you spot the typo from yesterday's [Zazzle infographic from Berlin July 2019 - 150px circular thumbnail from 168 thumbnails (12x14 = 1800px2100px)](http://rolandtanglao.com/2019/11/26/p1-zazzle-berlin-july-2019-info-graphic-circular-150-pixel-thumbnails/)?

* Yes `ls -1tr` instead of `ls -1` because the latter sorts by name instead of by time created which means yesterday's infographic was chronologically sorted instead of randomly sorted. Obviously I prefer the randomly sorted :-) #ymmv

## Colophon

From the [README](https://github.com/rtanglao/rt-berlin-july-2019/blob/master/README.md#november-26-2019):

```bash
mkdir 75x75
# set id is: 72157709917594396 which comes from the album url:
# https://www.flickr.com/photos/roland/albums/72157709917594396
./get-thumbnail-75-berlin-2019.rb 72157709917594396 2>/tmp/log.txt >berlin2019-url-75x75.txt
cd 75x75
cat ../berlin2019-url-75x75.txt  | ../backup75x75.rb
# 2100/75 = 28, 1800/75 = 24, 24 * 28 = 672
find . -type f | shuf -n672 > rt-berlin-july2019-672files.txt 
mkdir CIRCULAR
cat rt-berlin-july2019-672files.txt | parallel magick '{}' -vignette 0x0+0+0 'CIRCULAR/{}'
cd CIRCULAR
ls -1tr *.jpg > 672jpgs.txt
montage -verbose -adjoin -tile 24x28 +frame +shadow +label -adjoin -geometry '75x75+0+0<' @672jpgs.txt rt-berlin-12-14-75x75.jpg
```