---
layout: post
title: How I made my Make Vancouver Shirt
---

## Pontifications

(UPDATE: Here's [the followup blog post with the actual shirt](http://rolandtanglao.com/2016/12/29/p1-make-vancouver-shirt-result-fab/)!)

([I know I said I wouldn't blog until 2017](http://rolandtanglao.com/2016/12/23/p1-happy-holidays-2016/) but I could resist :-) !)
[Check out the repo for full details](https://github.com/rtanglao/makevancouver-flickr-2004-2012):

* Make Vancouver's help info requests 16" by 12" at 200dpi i.e. a 3200x2400  png: therefore using 10x10 thumbnails: 320*240=76800 thumbnails
* ```cd 10x10; ls -1 | head -76800 >1st76800pngs.txt```
* ```gm montage -verbose -adjoin -tile 320x240 +frame +shadow +label -adjoin -geometry '10x10+0+0<' @1st76800pngs.txt montage320x240-flickr-2004-2012-1st76800-10x10.png```
* upload montage320x240-flickr-2004-2012-1st76800-10x10.png to [make](https://www.makevancouver.com/), add it to 1x Unisex Adult American Apparel Mighty Print T-Shirt - M / Front  and change background colour to pink and done! I'll post a blog post as a followup!
* back to scheduled holiday non blogging :-)