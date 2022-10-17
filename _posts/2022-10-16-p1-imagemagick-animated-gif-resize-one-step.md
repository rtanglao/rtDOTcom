---
layout: post
title: "How to resize images and make an animated GIF in one step using imagemagick"
---

* [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/) Oct 12, 2022. 19:29 

```bash
~/bin/magick convert -delay 20 -loop 0 `ls -1 *.JPG` \
-resize 1200x675 12oct2022beeflying.gif 
```

^^-- resize and make animated gif in 1 step

### Previously

* October 9, 2022: [How to resize images to Twitter animated GIF dimensions and then make an animated GIF using imagemagick](http://rolandtanglao.com/2022/10/09/p1-how-to-resize-images-and-make-animated-gif-imagemagick/) <--- 2 step process!
