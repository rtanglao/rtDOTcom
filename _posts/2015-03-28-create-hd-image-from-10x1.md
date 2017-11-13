---
layout: post
title: How to use graphicsmagick to make an HD image from 10x1px JPEGs
---
because some images were small (< 10 colours?!?) had to use ‘1x1+0+0<‘. Without ‘1x1’, images less than 10px wide would have a 10 pixel border added!

    gm montage -verbose -tile 192x1080 +frame +shadow +label \
    -geometry ‘1x1+0+0<‘ @first_207360jpgs.txt hdframe.png
