---
layout: post
title: Mogrify works better to convert TIFF to PNG or use 'convert' one at a time with a for loop
---

## Pontifications
* Following on from yesterday's [How to convert all TIFFs to PNGs in a separate sub directory using ImageMagick / GraphicsMagick](http://rolandtanglao.com/2017/05/31/p1-convert-tif-to-jpg-using-graphicsmagick-imagemagick/), actually ```mogrify``` or ```convert``` one at a time in a for loop works better! A bug in batch ```convert``` perhaps?!?
* example:

```bash
# Warning mogrify will overwrite your files if you don't 
# change format or do something to create new filenames
# or put the files in a subdirectory
gm mogrify -format png *.TIF 
```