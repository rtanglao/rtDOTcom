---
layout: post
title: "Why do I need two extra bytes to make a 222x222 png using imagemagick (and why didn't this surface in 2016? 64 bit boundary issue? Padding issue? Little Endian? Big Endian?)"
---

* Why do I need two extra bytes to make a 222x222 png using `imagemagick` ?

* [Again](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/README.md#10april2021-two-extra-bytes-fixes-it-i-am-not-sure-why) :-) I don't understand why since 222*222 = 49,284 so I shouldn't need 49, 286 3 byte colour values right? Just 49 284 should be sufficient. What am I missing?
* Perhaps 64 bit boundary? Or little endian? big endian?

  ```bash
  % { printf "P6\n%d %d\n255\n" 222 222 ; cat 1st-49284-2020-2019-roland-flickr-average-colours.rgb} \
  | magick  - image88.png
  magick: unable to read image data `/var/folders/h0/m31kq8415wb50xg_7kwk06h40000gn/T/magick-2mCuD6a8H66a7qb5_WpeXHJ3uph3P9pv' @ error/pnm.c/ReadPNMImage/1442.
  % { printf "P6\n%d %d\n255\n" 222 222 ; cat 1st-49286-2020-2019-roland-flickr-average-colours.rgb} \
  | magick  - image88.png
  % # no error message i.e. it works!
  ```

* And why didn't this surface in 2016's blog post about this: [How to make a PNG file from an RGB file of ASCII Hex Colours made using xxd](http://rolandtanglao.com/2016/01/25/p3-using-convert-to-make-a-png-from-rgb-file/)

* And yes I am totally over-analyzing this :-) !

