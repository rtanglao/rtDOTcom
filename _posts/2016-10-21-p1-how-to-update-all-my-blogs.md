---
layout: post
title: How to update all my websites and blogs with hugo and jekyll and omni outliner
---
It's easier to find this on the internet if I post it here. Really should be part of [my forthcoming wiki](http://rolandtanglao.com/2016/09/24/p1-rolandex-for-my-personal-wiki/).

## rolandtanglao.com

```sh
cd /Users/rtanglao/Dropbox/ROLANDTANGLAO-DOT-COM-SURGE
# edit posts in _posts
jekyll build # --incremental after you add an entry
surge _site --domain rolandtanglao.com
```

## biketoworkshop.com

```sh
hugo server --theme=redlounge --buildDrafts --watch &
hugo --theme=redlounge  --buildDrafts
surge public --domain biketoworkshop.com
```

## rolandoutlines.com

```sh
cd /Users/rtanglao/DROPBOX/ROLAND-OUTLINES
# export to subdirectory using dynamic HTML to SURGE from Omni Outliner e.g. notes-roland-haskell_programming.oo
mv SURGE/notes-roland-haskell_programming.html/ SURGE/notes-roland-haskell_programming
surge SURGE  --domain rolandoutlines.com
```
