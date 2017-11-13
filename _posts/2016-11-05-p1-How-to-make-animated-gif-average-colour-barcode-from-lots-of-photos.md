---
layout: post
title: How To -- Animated GIF average colour 'Barcode' from lots of photos
---

tl;dr: it's not hard, you just need some photos :-)

## Pontifications

(side note: I use bullet lists because numerical lists are too hard to use with explanatory material ; the list element number gets reset and other issues!)

The animated GIF is for twitter so we'll see if the as of this writing current maximum twitter resolution 1024x512 will be less than 15MB the twitter maximum file size.

(All the source code including the file with the average colors, the 1024 line files, the 1024 x 512 line files, the raw RGB files, the PNG files and the animated gifs can be found on github at: [https://github.com/rtanglao/rt-animated-gifs/tree/master/2016-11-03](https://github.com/rtanglao/rt-animated-gifs/tree/master/2016-11-03)

* \#1 Get the photos (I got mine from my flickr stream 2004-2012 using the "easy" to use flickr API (if you can figure out how to do an HTTP GET in your favorite computer language it's "easy"; at least far easier and better documented than most APIs :-) )

* \#2 Convert 2004-2012 roland flickr thumbnails to one file with 1 average colour RGB hex value per line using imagemagick scaling 10 1px by 1 px (another aside: which is better graphicsmagick or imagemagick?) <br />
```./printAverageColourHexValueFromDirectory.rb /Users/rtanglao/Dropbox/Public/CCC/DATASETS/09April2012-ROLAND-103K-75x75-FLICKR-PHOTOS/75X75/FILES_SYM_LINKED_SEQUENTIALLY/ > flickr-roland-2004-12-avgcolour.txt ``` 

* \#3 Split into files 1024 lines long (since we intend to make 1024 pixel wide 'barcodes' <br />
```-a3``` means 3 digits e.g. 001 and then 002, ```-l 1024``` means 1024 line chunks, ```--numeric-suffixes=1``` means start the file numbering at 1 instead of 0 <br />
 ```gsplit -a3 -l 1024 --numeric-suffixes=1  flickr-roland-2004-12-avgcolour.txt 1024line-chunks-flickr-roland-2004-12-avgcolour-``` ([more info on split/gsplit and GNU utilities on OS X](http://rolandtanglao.com/2016/11/06/p1-linux-core-utilities-instead-of-osx-bsd-utilities/))
 
* \#4 move into a separate directory to make things easier and cleaner <br />
```mkdir 1024FILES; cd !$; mv ../1024line-ch* .```

* \#5 create a separate directory for images and working files <br />
```mkdir 1024x512```

* \#6 Change the 1024 pixel file into a 1024x512 pixel file <br />
```parallel "for i in {1..512};do cat {} >>1024x512/{.}.txt; done" ::: 1024line-chunks-flickr-roland-2004-12*```

* \#7 ```cd 1024x512```

* \#8 Turn the files of pixel colours into raw RGB files<br />
```parallel "xxd -r -p {} {.}.rgb" ::: 1024line-chunks-flickr-roland-2004-12-avgcolour-*.txt```

* \#9 Convert the RGB raw files into PNG files:  <br />
```parallel "gm convert -depth 8  -size 1024x512 {} {.}.png" ::: 1024line-chunks-flickr-roland-2004-12-avgcolour-*.rgb```

* \#10 This is what we want but unfortunately it's 45MB! Too big for twitter <br />
```gm convert -loop 50 -delay 20 *.png flickr2004-12-roland-avg-colour-barcode.gif``` 

* \#11 Halve the resolution from 1024x512 to 512x256 and then you get a nice 9MB file<br />
```gm convert -loop 50 -delay 20 -scale 512x256 *.png 512x256-flickr2004-12-roland-avg-colour-barcode.gif```

* \#12 do a little dance done :-)

## Output

![animated GIF of roland's flickr average colour barcode 2004-2012](https://c2.staticflickr.com/6/5629/30170047903_3d6757bd08_o_d.gif "animated GIF of roland's flickr average colour barcode 2004-2012")


