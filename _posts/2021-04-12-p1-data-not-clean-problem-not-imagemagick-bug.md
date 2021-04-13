---
layout: post
title: "Not an imagemagick bug but an unclean data problem: one of the rows is missing an average colour because there was no thumbnail in flickr"
---
* Yesterday in [Why do I need two extra three byte values to make a 222x222 png using  imagemagick (and why didn't this surface in 2016? 64 bit boundary issue?  Padding issue? Little Endian? Big Endian?)](http://rolandtanglao.com/2021/04/11/p1-why-two-extra-bytes-to-make-222-222-png-using-imagemagick/) I was wrong. Not an `imagemagick` issue it turns out but a an unclean data problem; one of the rows is missing an average colour because there was no thumbnail in `flickr`. No thumbnail  means nothing to compute the average colour of so the row is blank in the dataset! Fixed it by removing that one row using `grep`

# Details
## 12april2021 figured it out, it's my non clean data :-)
* remove the one row i.e. row 19907 without a thumbnail and therefore without an average colour and then go from there!
```bash
grep  "#" 2020-and-2019-roland-flickr-imagemagick-average-colours.txt \
> missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.txt
head -n 49284 missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.txt \
>49284-missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.txt
xxd -l 49284 -u -r -p \
49284-missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.txt \
> 49284-missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.rgb
magick -depth 8 -size 222x222 \
49284-missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.rgb \
49284-missing-thumbnail-with-missing-avgcolour-removed-2020-and-2019-roland-flickr-imagemagick-average-colours.png
```

## 12april2021 probably not an imagemagick but a bug in my data aka i forgot that the average colour is missing for 1 row!

* row 19907 doesn't have an average colour because flickr doesn't have a thumbnail!
```bash
% grep -C 3 -vn "#" 1st-49284-2020-2019-roland-flickr-average-colours.txt 
19904-#333436
19905-#AAABAD
19906-#AFAFAF
19907:
19908-#A7A9AA
19909-#B7B8B7
19910-#B5B6B6
```
