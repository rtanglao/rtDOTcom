---
layout: post
title: "Average colour according to imagemagick resize of my flickr photos Jan 1, 2019 - Dec 31, 2020"
---

# TL;dr
I have average colour of my photos arranged chronologically January 1, 20219 - December 31, 2020. It may be wrong, need to double check :-) This is the output of photoshop in interleaved mode, 3 channels (R, G, B)

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51097868917/in/datetaken-public/" title="january 1, 2019, december 31, 2020-interlaced-2020-and-2019-roland-flickr-imagemagick-average-colours"><img src="https://live.staticflickr.com/65535/51097868917_20d09df39f_m.jpg" width="222" height="222" alt="january 1, 2019, december 31, 2020-interlaced-2020-and-2019-roland-flickr-imagemagick-average-colours"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

# Extra Bonus "glitch" art

* when you don't use interleave mode in Photoshop

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51097868912/in/datetaken-public/" title="wrong aka glitch art :-) 2020-and-2019-roland-flickr-imagemagick-average-colours"><img src="https://live.staticflickr.com/65535/51097868912_dcaff22a34_m.jpg" width="222" height="222" alt="wrong aka glitch art :-) 2020-and-2019-roland-flickr-imagemagick-average-colours"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

# Details

## 05april2021 still not sure why imagemagick doesn't work, maybe because the header is missing or maybe because it doesn't end with '.raw'?
* add the header as per this stack overflow question, [Converting raw images without headers](https://stackoverflow.com/questions/62602215/converting-raw-images-without-headers)?
```bash
{ printf "P6\n%d %d\n255\n" WIDTH HEIGHT ; cat YOURFILE; } > result.ppm
```
* or use `ffmpeg` as per this stack overflow question, [Convert raw RGB32 file to JPEG or PNG using FFmpeg](https://stackoverflow.com/questions/46310408/convert-raw-rgb32-file-to-jpeg-or-png-using-ffmpeg)?
```bash
ffmpeg -f rawvideo -pixel_format rgba -video_size 320x240 -i input.raw output.png #i would use rgb instead of rgba
```

## 05april2021 the file has to be called .raw to be opened in photoshop in interleaved mode

* renamed `2020-and-2019-roland-flickr-imagemagick-average-colours.rgb` to:
`2020-and-2019-roland-flickr-imagemagick-average-colours.raw` and opened in photoshop in interleaved mode, 3 channels, 222x222pixels and it worked!
* here is the PNG which worked: [https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/THUMBS_75X75/interlaced-2020-and-2019-roland-flickr-imagemagick-average-colours.png](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/THUMBS_75X75/interlaced-2020-and-2019-roland-flickr-imagemagick-average-colours.png)
* if you select non interleaved mode, then it doesn't work but you get glorious glitch art: [https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/THUMBS_75X75/2020-and-2019-roland-flickr-imagemagick-average-colours.png](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/THUMBS_75X75/2020-and-2019-roland-flickr-imagemagick-average-colours.png)

## 03april2021 hilariously gnuplot works

* see [http://gnuplot.sourceforge.net/demo_4.4/image.1.gnu](http://gnuplot.sourceforge.net/demo_4.4/image.1.gnu) which is an example from: http://gnuplot.sourceforge.net/demo_4.4/image.html

```
plot '2020-and-2019-roland-flickr-imagemagick-average-colours.rgb' binary array=222x222 flipy format='%uchar' with rgbimage
```

output: [https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/THUMBS_75X75/gnuplot-2020-and-2019.png](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/THUMBS_75X75/gnuplot-2020-and-2019.png)

## 03april2021 create file of colours and then raw file and then png

* 1\. remove the one bad file which has `synth_75sqisvalid` set to `0` aka `false`
```bash
mlr --csv cut -f synth_75imaveragecolour,synth_75sqisvalid \
../../files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-filename-imagemagick-avg-colour-metadata.csv\
| grep -v ",0" | wc -l
49549
mlr --csv cut -f synth_75imaveragecolour,synth_75sqisvalid \
../../files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-filename-imagemagick-avg-colour-metadata.csv\
> 2020-and-2019-roland-flickr-imagemagick-average-colours.csv
mlr --csv cut -f synth_75imaveragecolour \
>  2020-and-2019-roland-flickr-imagemagick-average-colours.csv\
>  | tail -n +2 >2020-and-2019-roland-flickr-imagemagick-average-colours.txt
```
* 2\. create raw file
```bash
#xxd -r -p 2020-and-2019-roland-flickr-imagemagick-average-colours.txt \
2020-and-2019-roland-flickr-imagemagick-average-colours.rgb
# 222 x 222 = 49284
xxd -l 49284 -u -r -p \
2020-and-2019-roland-flickr-imagemagick-average-colours.txt 2020-and-2019-roland-flickr-imagemagick-average-colours.rgb
```
* 3\. create png
* square root of 49549 is approximately 222
```bash
magick convert -depth 8  -size 222x222 2020-and-2019-roland-flickr-imagemagick-average-colours.rgb\
 2020-and-2019-roland-flickr-imagemagick-average-colours.png
```
* fails on ubuntu 20.04 with convert and on macOS catalina with magick:

```bash
convert -size 222x222 -depth 8 RGB:2020-and-2019-roland-flickr-imagemagick-average-colours.rgb image.png
convert-im6.q16: unexpected end-of-file `2020-and-2019-roland-flickr-imagemagick-average-colours.rgb': No such file or directory @ error/rgb.c/ReadRGBImage/242.
convert-im6.q16: no images defined `image.png' @ error/convert.c/ConvertImageCommand/3258.
```

## 03april2021 imagemagick average colour worked?!?

```bash
roland@Rolands-MacBook-Air THUMBS_75X75 % bundle exec ../get-filename-imagemagick-average-colour-from-75x75thumbnail.rb \
../../files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-metadata.csv \
../../files_too_big_for_github_rt-flickr-sqlite-csv/2020-and-2019-roland-flickr-filename-imagemagick-avg-colour-metadata.csv
```

## 03april2021 current plan
* I don't trust myself :-)  to take the 100% care needed to get `csvjoin` to work, it's easy to mess up
* so i will add the column from ruby and in fact have multiple columns
    * synth_75sqfilename (the filename of the 75x75 thumbnail)
    * synth_75imaveragecolour (average colour by resizing to 1x1 in imagemagick)
    * synth_75sqisvalid (in case the thumbnail is not a valid jpeg or png), 1 = valid, 0 = invalid (there's only 1 invalid 75x75px thumbnail from all 45000 2019-2020 photos

## 03april2021 csvjoin does add columns like i want

```bash
roland@Rolands-MacBook-Air THUMBS_75X75 % cat testcsv.csv 
column1
samplecolumn1value
roland@Rolands-MacBook-Air THUMBS_75X75 % cat column2.csv 
column2
samplecolumn2value
roland@Rolands-MacBook-Air THUMBS_75X75 % csvjoin testcsv.csv column2.csv
column1,column2
samplecolumn1value,samplecolumn2value
```




