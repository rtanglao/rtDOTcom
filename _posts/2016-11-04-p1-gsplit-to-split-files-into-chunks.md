---
layout: post
title: want to split text files into chunks? gsplit on OS X split on linux! 
---

World of unix :-) split for linux, gsplit for OS X

## Pontifications

You can see how i used this by [going to https://github.com/rtanglao/rt-animated-gifs and scrolling down to November 4, 2016](https://github.com/rtanglao/rt-animated-gifs).

* ```brew install coreutils``` on os x if you use homebrew similar incantations for other package managers
* ```gsplit -a3 -l 1024 --numeric-suffixes=1  flickr-roland-2004-12-avgcolour.txt 1024line-chunks-flickr-roland-2004-12-avgcolour-``` # -a3 means 3 digits i.e. ```nnn``` e.g. 001 , -l 1024 means 1024 line chunks, --numeric-suffixes=1 means start at 1 instead of 0

