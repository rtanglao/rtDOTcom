---
layout: post
title: "Make artofwhere tights with gray patches and pink aka adventures in issue oriented development "
---
* See [rt-flickr-sqlite-csv issue #1, Make artofwhere tights with gray patches and pink](https://github.com/rtanglao/rt-flickr-sqlite-csv/issues/1)

* Copy and Pasted from github for future reference
- [x] Make gray legs
```bash
cd /Users/roland/Documents/GIT/rt-flickr-sqlite-csv/GRAY_ONLY_75PX_BY_75PX_PATCHES
mkdir GRAY_PATCHES_WITH_PINK_BACKGROUND 
cd GRAY_PATCHES_WITH_PINK_BACKGROUND
find .. -name 'gray_only_geomencircle_second_of_day_no_theme_no_caption_roland_flickr_2019_2020.pn*.jpg' \
-print  | shuf -n 3825 > right-leg-shuffled-3825-gray-2019-20-jpgs.txt
find .. -name 'gray_only_geomencircle_second_of_day_no_theme_no_caption_roland_flickr_2019_2020.pn*.jpg' \
-print  | shuf -n 3825 > left-leg-shuffled-3825-gray-2019-20-jpgs.txt
montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
-geometry '75x75+0+0<' @right-leg-shuffled-3825-gray-2019-20-jpgs.txt \
right-leg_artofwhere-gray-2019-20.png
montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
-geometry '75x75+0+0<' @left-leg-shuffled-3825-gray-2019-20-jpgs.txt \
left-leg_artofwhere-gray-2019-20.png
```
- [x] Change the background colour to pink
```bash
magick right-leg_artofwhere-gray-2019-20.png -fuzz 25% -fill pink \
-opaque white -flatten pink-background-right-leg_artofwhere-gray-2019-20.png
magick left-leg_artofwhere-gray-2019-20.png -fuzz 25% -fill pink \
-opaque white -flatten pink-background-left-leg_artofwhere-gray-2019-20.png
```
- [x] Upload to Art of Where - DONE ! Order `du9w3h`, GET YOURS TODAY :-) -> [https://artofwhere.com/artists/roland-tanglao/clothing/leggings/5819934]( https://artofwhere.com/artists/roland-tanglao/clothing/leggings/5819934)

### Finished Graphics:

Left Leg:

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/52533121870/in/dateposted-public/" title="pink-background-left-leg_artofwhere-gray-2019-20"><img src="https://live.staticflickr.com/65535/52533121870_edb80f65e9_w.jpg" width="212" height="400" alt="pink-background-left-leg_artofwhere-gray-2019-20"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

Right Leg:

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/52532929359/in/dateposted-public/" title="pink-background-right-leg_artofwhere-gray-2019-20"><img src="https://live.staticflickr.com/65535/52532929359_8a48f3cda3_w.jpg" width="212" height="400" alt="pink-background-right-leg_artofwhere-gray-2019-20"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>




### Previously

* November 26, 2022: [Simon  Willison: Massively increase your productivity on personal projects  with comprehensive documentation and automated tests aka issue oriented  development including tests for documentation!](http://rolandtanglao.com/2022/11/26/p1-simon-willison-issue-oriented-development-including-documentation-tests/)        
