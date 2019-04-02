---
layout: post
title: "Tried Jean Fan's R function on Mozlando KSC 200x200px, maybe I should have started with a black and white image?"
---

# Pontifications

* The output below is great but maybe I should have started with a black and white i.e. converted the image from colour to black and white first?
* And maybe I could use the output images for [white camo](http://rolandtanglao.com/2019/01/28/p1-green-tan-white-camoflage-from-vancouver-flickr-pictures/)?
*  See: [Use Hatching, shape-based tonal or shading, to create fun infographics for tshirts in R (code by Jean Fan)](http://rolandtanglao.com/2019/03/31/p1-use-hatching-to-create-fun-infographics-for-tshirts/)
*  Here is what I did:

```bash
convert 2019-01-31-05-36-oily-200x200-out.png 2019-01-31-05-36-oily-200x200-out.jpg
```

```r
setwd("~/GIT/rt-mozlando2018-ksc")
source('hatching.R')
img <- readJPEG("/home/roland/GIT/rt-mozlando2018-ksc/TRY2-200x200OILY/2019-01-31-05-36-oily-200x200-out.jpg")
hatching(img, size=0.1, var=0.5, N=10000, pch=0, step=0.01)
# export as 3600 px wide to
# https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/hatched-2019-01-31-05-36-oily-200x200-out.png
img2 <- readJPEG("/home/roland/GIT/rt-mozlando2018-ksc/TRY2-200x200OILY/2019-01-31-05-36-oily-200x200-out.jpg")[,,1]
img2 <- t(apply(img2,2,rev))
hatching(img2)
# export as 3600 px wide to
# https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/hatched2-2019-01-31-05-36-oily-200x200-out.png
```

## Output hatched-2019-01-31-05-36-oily-200x200-out.png

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/47512303491/in/dateposted-ff/" title="hatched-2019-01-31-05-36-oily-200x200-out"><img src="https://farm8.staticflickr.com/7832/47512303491_b046dc3f84.jpg" width="500" height="434" alt="hatched-2019-01-31-05-36-oily-200x200-out"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>


## Output hatched2-2019-01-31-05-36-oily-200x200-out.png

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/47512306271/in/dateposted-ff/" title="hatched2-2019-01-31-05-36-oily-200x200-out"><img src="https://farm8.staticflickr.com/7867/47512306271_af67cc6af6.jpg" width="500" height="434" alt="hatched2-2019-01-31-05-36-oily-200x200-out"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>