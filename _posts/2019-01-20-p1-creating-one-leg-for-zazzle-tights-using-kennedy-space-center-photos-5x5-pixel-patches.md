---
layout: post
title: "Creating one leg for Zazzle / Art of Where tights using random 5x5 pixel patches from Kennedy Space Center Photos"
---
# Pontifications

(see Earlier post: [Next Art of Where Tights 3325px x 6358px for one leg : 5x5 random pixels from Space Shuttle Atlantis photos](http://rolandtanglao.com/2019/01/11/p1-artofwhere-tights-using-space-shuttle-atlantis-5x5-pixels/))

* 3325 / 5 px = 665 rows one way i.e. "horizontally"
* 6358 -> 6370 / 5 px = 1274 rows the other way "vertically"
* each original is 4608 x 3456 px
* round down to 4605 x 3455 px
  * which means there are 921 five pixel columns horizontally
  * and 691 five pixel rows vertically
* which means the script needs to pick 847210 (665 * 1274) random 5px x 5x patches
* use the imagemagick ```crop``` commmand with the ```+repage``` option 
see: [http://www.imagemagick.org/Usage/crop/#crop_repage](http://www.imagemagick.org/Usage/crop/#crop_repage)
e.g.

```bash
  convert rose: -crop 40x30+40+30  +repage  repage_br.gif
```
  
* in our case something like:
  
```bash
  convert <ksc_img> -crop 5x5+<random_x>+<random_y>  +repage  5x5-ksc.png
```