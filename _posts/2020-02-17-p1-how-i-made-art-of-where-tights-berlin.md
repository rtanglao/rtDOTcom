---

layout: post
title: "How I made Art of Where Tights from Berlin photos"
---

# Pontifications

* Through a long and labourious process :-)
* Actually it's just a mashup of what came before :-)  (white [kennedy space center tights](http://rolandtanglao.com/2019/04/07/p1-white-pseudo-camo-artofwhere-tights-from-mozlando2018-ksc-hatched-photos/), [5x5 patches from KSC](http://rolandtanglao.com/2019/01/20/p1-creating-one-leg-for-zazzle-tights-using-kennedy-space-center-photos-5x5-pixel-patches/) which turned out to impractical so we went with [100x100](http://rolandtanglao.com/2019/01/25/p1-patchwork-quilt-effect-is-better-with-100-pixel-by-100-pixel-patches/)). The following is a modified version of  [https://github.com/rtanglao/rt-berlin-january-2020/blob/master/README.md](https://github.com/rtanglao/rt-berlin-january-2020/blob/master/README.md ) 
* Here's how it looks:

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/49549249887/in/dateposted-public/" title="&quot;Black-ish&quot; high-quality-artofwhere-berlin2020-leggings"><img src="https://live.staticflickr.com/65535/49549249887_76cbabcaf1_w.jpg" width="400" height="173" alt="&quot;Black-ish&quot; high-quality-artofwhere-berlin2020-leggings"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## 16february2020 artofwhere.com tights

* 1\. create circular thumbnails

```bash
mkdir BLACK_CIRCULAR
mlr --csv --implicit-csv-header --headerless-csv-output \
cut -f 1 black-berlin-january2020.txt > just-black-files-berlin-january2020.txt
cat just-black-files-berlin-january2020.txt | \
parallel magick '{}' -vignette 0x0+0+0 'BLACK_CIRCULAR/{/}'
```

* 2\. make artofwhere graphic
    * 3400 / 75 px = 46 rows one way i.e. "horizontally"
    * 6400 / 75 px = 86 rows the other way "vertically"
    * 46 * 86 = 3956 circular thumbnails

```bash
cd BLACK_CIRCULAR
ls -1 *.jpg | shuf -n 3825 > right-leg-shuffled-3825-black-jpgs.txt
ls -1 *.jpg | shuf -n 3825 > left-leg-shuffled-3825-black-jpgs.txt
montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
-geometry '75x75+0+0<' @right-leg-shuffled-3825-black-jpgs.txt \
right-leg_artofwhere_berlin_jan_2020.png
montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
-geometry '75x75+0+0<' @left-leg-shuffled-3825-black-jpgs.txt \
left-leg_artofwhere_berlin_jan_2020.png
```
## 15february2020 get average color of patches

* 1\. get average color

a) first get filenames of the patches

```bash
ls -d /home/rtanglao/GIT/rt-berlin-january-2020/75PX_BY_75PX_PATCHES/*.jpg  \
> berlin_jan2020_75x75_jpg_filenames.txt
```

b) then get average color of the patches

```bash
cat berlin_jan2020_75x75_jpg_filenames.txt  | \
../print-file-colorname-hex-color.rb > berlin_jan2020_file_colorname_hexcolor.csv
```

c) to get an idea of the number of each colour, cut out the'file' field which is unique

```bash
mlr --csv cut -x -f 'file' *.csv | more
grep black  berlin_jan2020_file_colorname_hexcolor.csv > black-berlin-january2020.txt
grep red  berlin_jan2020_file_colorname_hexcolor.csv > red-berlin-january2020.txt
grep green  berlin_jan2020_file_colorname_hexcolor.csv > gren-berlin-january2020.txt
grep blue  berlin_jan2020_file_colorname_hexcolor.csv > blue-berlin-january2020.txt
```

d) create a file with just the red filenames, no colour or hex colour fields

```bash
mlr --csv --implicit-csv-header --headerless-csv-output \
cut -f 1 black-berlin-january2020.txt > just-blackfiles-berlin-january2020.txt
```

e) make black circular thumbnails

```bash
mkdir BKACK_CIRCULAR
cat just-red-files-berlin-january2020.txt | \
parallel magick '{}' -vignette 0x0+0+0 'BLACK_CIRCULAR/{/}'
```

## 09february2020

* 1\. how to crop an image to 75x75
  * 2000, 2000 is the offset from top left (gleaned from [How to crop an image using imagemagick from the command line?](https://superuser.com/questions/1161340/how-to-crop-an-image-using-imagemagick-from-the-command-line))
  * ```magick``` replaces ```convert -crop``` in imagemagick 7


```bash
magick dsc_3671_49469147273_o.jpg -crop 75x75+2000+2000 +repage croptest.jpg
```

* 2\. use pixel_x_dimension and pixel_y_dimension from https://github.com/tonytonyjan/exif get width and height

* 3\. use this file list:

```bash
ls -d /mnt/c/Users/rtang/Pictures/23-31JANUARY2020-BERLIN-ALL_HANDS/*.jpg > berlin_jpg_filenames.txt
```

* 4\. Create CSV file with max x and max y for 75 pixel by 75 pixel

```bash
/print-file-width-length-max75-x-max75-y.rb berlin_jpg_filenames.txt > berlin-75px-75px-max-x-maxy.txt
```

* 5\. Create 1000 75px by 75 px patches. Maybe do 1000 at a time for a total of 10,000 <--- I actually did approximately 20,000

```bash
mkdir 75PX_BY_75PX_PATCHES
cd !$
../create-75px-75px-patches.rb ../berlin-75px-75px-max-x-maxy.txt 1000
../create-75px-75px-patches.rb ../berlin-75px-75px-max-x-maxy.txt 9000
../create-75px-75px-patches.rb ../berlin-75px-75px-max-x-maxy.txt 1000
```

