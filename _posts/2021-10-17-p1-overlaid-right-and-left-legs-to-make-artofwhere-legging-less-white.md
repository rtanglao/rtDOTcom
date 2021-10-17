---
layout: post
title: "I made artofwhere leggings from my red-ish and pink-ish flickr photos 2019-2020"
---

* I took the left and right legs from the previous post : [Make the legs for artofwhere tights using red pink flickr 2019-2020](http://rolandtanglao.com/2021/10/16/p1-roland-flickr-2019-2020-red=pink-artofwhere-tights/) and overlaid them using imagemagick and then uploaded the graphic as the left leg and cloned it to the right leg.
* You can order them from art of where here: [artofwhere.com/artists/roland-tanglao/clothing/leggings/5038278](https://artofwhere.com/artists/roland-tanglao/clothing/leggings/5038278)
* Here are the `imagemagick` commands from my [github flickr sqlite repo](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/README.md#17october20201-too-much-white-colour-so-overlay-to-make-a-more-colourful-leg) I used to to do this:
```bash
magick convert right-leg_artofwhere-red-pink-2019-20.png -transparent "#ffffff" transparent-right-leg_artofwhere-red-pink-2019-20.png
magick convert left-leg_artofwhere-red-pink-2019-20.png -transparent "#ffffff" transparent-left-leg_artofwhere-red-pink-2019-20.png
magick convert -background none -layers flatten  transparent-right-leg_artofwhere-red-pink-2019-20.png transparent-left-leg_artofwhere-red-pink-2019-20.png transparent-artofwhere_left_and_right_overlaid-red-pink-2019-2020.png
```
* `right-leg_artofwhere-red-pink-2019-20.png` comes from [Make the legs for artofwhere tights using red pink flickr 2019-2020](http://rolandtanglao.com/2021/10/16/p1-roland-flickr-2019-2020-red=pink-artofwhere-tights/)  ; same with the left leg
    * Which in turn come from [red_pink_geomencircle_second_of_day_no_theme_no_caption_roland_flickr_2019_2020.R](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/red_pink_geomencircle_second_of_day_no_theme_no_caption_roland_flickr_2019_2020.R) as blogged in: [New  informal rules: name the R script the same as the output graphic, post  it to flickr and use a small dataset using red pink average colour  example from 2019-2020 flickr average colour](http://rolandtanglao.com/2021/10/02/p1-small-dataset-name-plot-same-as-r-script/)        

## Art of Where 3D Embed

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51600971695/in/datetaken-public/" title="3D artofwhere-flickr-2019-2020-red-pink-leggings"><img src="https://live.staticflickr.com/65535/51600971695_3985036063.jpg" width="500" height="446" alt="3D artofwhere-flickr-2019-2020-red-pink-leggings"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## Individual Leg Embed

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51600665910/in/datetaken-public/" title="transparent-artofwhere_left_and_right_overlaid-red-pink-2019-2020"><img src="https://live.staticflickr.com/65535/51600665910_dd799d49c3.jpg" width="265" height="500" alt="transparent-artofwhere_left_and_right_overlaid-red-pink-2019-2020"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>