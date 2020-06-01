---
layout: post
title: "How I made Art of Where Tights aka leggings and mask from Vancouver 2020 Pink Petal photos" 
---

# Pontifications

* Here are the tights I made! Want to order your own? Please [click this link to order the leggings from Art of Where in Montréal](https://artofwhere.com/artists/roland-tanglao/clothing/leggings/3502475)):

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/49958727272/in/dateposted-public/" title="vancouver-pink-petal-2020-aow-tights-social-media-15909812586846654058"><img src="https://live.staticflickr.com/65535/49958727272_bc9dc91645.jpg" width="500" height="446" alt="vancouver-pink-petal-2020-aow-tights-social-media-15909812586846654058"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* Here is the mask  I made! Want to order your own? Please [click this link to order a mask from Art of Where in Montréal](https://artofwhere.com/artists/roland-tanglao/accessories/face-covering/3502516):

<a data-flickr-embed="true" href="https://www.flickr.com/photos/roland/49957949818/in/dateposted-public/" title="vancouver-pink-petal-2020-mask-15909828343118069753"><img src="https://live.staticflickr.com/65535/49957949818_2397f59b2c.jpg" width="500" height="446" alt="vancouver-pink-petal-2020-mask-15909828343118069753"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* You can find the source images at:

  * [https://www.flickr.com/photos/roland/albums/72157714184799381](https://www.flickr.com/photos/roland/albums/72157714184799381)

  ## 31may2020 create the left and right leg graphics

  * 1\. 3825 jpegs per leg (and then upload to artofwhere.com)

  ```bash
  ls -1 *.jpg | shuf -n 3825 > right-leg-shuffled-3825-pink-petal-jpgs.txt
  ls -1 *.jpg | shuf -n 3825 > left-leg-shuffled-3825-pink-petal-jpgs.txt
  montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
  -geometry '75x75+0+0<' @right-leg-shuffled-3825-pink-petal-jpgs.txt \
  right-leg_artofwhere-pink-petal-2020.png
  montage -verbose -adjoin -tile 45x85 +frame +shadow +label -adjoin \
  -geometry '75x75+0+0<' @left-leg-shuffled-3825-pink-petal-jpgs.txt \
  left-leg_artofwhere-pink-petal-2020.png
  ```

  ## 31may2020 create the  thumbnails
  as per: [http://rolandtanglao.com/2020/02/17/p1-how-i-made-art-of-where-tights-berlin/](http://rolandtanglao.com/2020/02/17/p1-how-i-made-art-of-where-tights-berlin/)

  * 1\. get the filenames
  ```bash
  ls -d /home/roland/GIT/rt-pink-petal-power/ORIGINALS/*.jpg > pink_petal_power_jpg_filenames.txt
  ```
  * 2\.get the maximum number of 75x75 positions in each original file
      * i am lazy so i just copied in https://github.com/rtanglao/rt-berlin-january-2020/blob/master/print-file-width-length-max75-x-max75-y.rb to this directory
  ```bash
  ./print-file-width-length-max75-x-max75-y.rb pink_petal_power_jpg_filenames.txt \
  > pink-petal-power-75px-75px-max-x-maxy.txt
  ```

  * 3\. make the 75x75 pixel thumbnails

  ```bash
  mkdir 75PX_BY_75PX_PATCHES
  cd !$
  ../create-75px-75px-patches.rb ../pink-petal-power-75px-75px-max-x-maxy.txt 10000
  ```
