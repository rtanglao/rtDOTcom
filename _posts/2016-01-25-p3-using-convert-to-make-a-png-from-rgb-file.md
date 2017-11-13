---
layout: post
title: How to make a PNG file from an RGB file of ASCII Hex Colours made using xxd
---
Notes:

1. -depth 8 means 8 bits per RGB value
2. 1158 is sqrt(wc -l 24jan2016-try-ig-vancouver-2015-dominant-colours.txt)


``` bash
convert -depth 8  -size 1158x1158 24jan2016-try-ig-vancouver-2015-dominant-colours.rgb 1158x1158-24jan2016-try-ig-vancouver-2015-dominant-colours.png
```
                                                                                                                                                                          