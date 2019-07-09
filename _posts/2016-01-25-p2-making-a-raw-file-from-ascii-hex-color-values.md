---
layout: post
title: How to make a RAW file from a file of ASCII Hex Colours using xxd
---
If you have a hex file of colours e.g. [48% of instagram 2015 vancouver dominant colours](https://github.com/rtanglao/rtgram/blob/master/THUMBNAIL_150x150/48percent-687858photo-ig-vancouver-2015-dominant-colours.txt), here’s how to use [xxd](http://linux.die.net/man/1/xxd) to do it ("-r" to create the hex dump, -p to take the ascii values):

``` bash
xxd -r -p ig-vancouver-2015-dominant-colours.txt ig-vancouver-2015-dominant-colours.try3.rgb
```
                                                                                                                                                                          