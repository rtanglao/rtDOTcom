---
layout: post
title: "Make the legs for artofwhere tights using red pink flickr 2019-2020"
---

* flickr: [left leg](https://flic.kr/p/2mBwyYR), [right leg](https://flic.kr/p/2mBoYfV)
* It's too white and not red/pink so overlay images on top of each other to get more colour, let's try that next

## Imagemagick fun
```bash
find . -name '*.jpg' -print  | shuf -n 3825 > right-leg-shuffled-3825-red-pink-2019-20-jpgs.txtls -1 *.jpg | shuf -n 3825 > left-leg-shuffled-3825-red-pink-2019-20-jpgs.txt
find . -name '*.jpg' -print  | shuf -n 3825 > left-leg-shuffled-3825-red-pink-2019-20-jpgs.txt
montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
-geometry '75x75+0+0<' @right-leg-shuffled-3825-red-pink-2019-20-jpgs.txt \
right-leg_artofwhere-red-pink-2019-20.png
montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
-geometry '75x75+0+0<' @left-leg-shuffled-3825-red-pink-2019-20-jpgs.txt \
left-leg_artofwhere-red-pink-2019-20.png
```
## Flickr embed Left Leg

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51597869569/in/datetaken-public/" title="left-leg_artofwhere-red-pink-2019-20"><img src="https://live.staticflickr.com/65535/51597869569_c5134ff4f1.jpg" width="265" height="500" alt="left-leg_artofwhere-red-pink-2019-20"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## Flickr embed Right Leg

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/51596386977/in/datetaken-public/" title="right-leg_artofwhere-red-pink-2019-20"><img src="https://live.staticflickr.com/65535/51596386977_1ec1564012.jpg" width="265" height="500" alt="right-leg_artofwhere-red-pink-2019-20"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
