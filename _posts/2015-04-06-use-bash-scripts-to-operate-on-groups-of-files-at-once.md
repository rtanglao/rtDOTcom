---
layout: post
title: How to use bash to operate on groups of files using GraphicsMagick?
---
If you want to operate on 9600 1 pixel by 1 pixel files at a time to form HD-width frames (i.e. 1920px wide) with GraphicsMagick (1920 pixels per row *5rows = 9600), here’s a [bash script](https://github.com/rtanglao/rtgram/blob/gh-pages/IG-VANCOUVER_2014/RENUMBERED/TOP10/TOPCOLOUR/make1920By5PixelPNG.sh):

    #!/bin/bash
    files=(*.jpg )
    frame=0
    for ((i=0; i<${#files[*]}; i+=9600)); do
      let “frame++”
      gm montage -verbose -tile 1920x5 +frame +shadow +label \
      -geometry 1x1+0+0 “${files[@]:i:9600}”\
      `printf “frame-%5.5u.png” “$frame”`
    done

1.  Why not just do this with ruby? Because bash is lighter weight
2.  Why do so few and split up into “frames”? Because graphicsmagick takes up lots of memory and runs slowly when you try to do all files in 1 big command line invocation.
