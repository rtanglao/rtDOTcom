---
layout: post
title: How to use graphicsmagick and xargs to crop top left most pixel
---
Since [I couldn’t get the mini_magick ruby gem](https://github.com/rtanglao/rtgram/blob/gh-pages/IG-VANCOUVER_2014/RENUMBERED/TOP10/createTopColour.rb) to work (file not found aka the ‘identify’ command couldn’t recognize jpeg files for some strange reason), i resorted to good ‘ole xargs:

    find . -maxdepth 1 -name ‘*.jpg’ -print0 | \
    xargs -0 -I file gm convert -crop 1x1+0+0 file TOPCOLOUR/file