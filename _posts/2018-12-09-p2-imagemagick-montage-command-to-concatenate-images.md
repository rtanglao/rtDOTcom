---
layout: post
title: "How To: Use imagemagick montage command to concate images"
---
## Pontifications

* From [September 11, 2016](http://rolandtanglao.com/2016/09/08/p1-24-squares-1-per-hour/), the important things in the ```gm montage``` or equivalently the ```imagemagick montage``` comnand are:
  * ```-adjoin``` leaves no spaces
  * ```-tile 7x6``` arranges the images in 7 columns by 6 rows
  * ```+shadow``` means no shadow
  * ```+label``` means no label
  * ```-geometry '1023x684+0+0<'``` means 1024 x 768 ? is this a bug? should it be ```768``` instead of ```684```?
  * ```null:``` is a placeholder blank image to pad out the first and last rows 
  
  
### 24 squares per day
1. ```cd /Users/rtanglao/Dropbox/GIT/2016-r-rtgram/JANUARY2016/24SQUARES-PER-DAY```
2. ```parallel Rscript ../../twenty-four-square-pie-chart-from-csv.R '{}' ::: ../??-january2016-ig-van-avgcolour-id-mf-month-day-daynum-unixtime-hour.csv```
3. ```mkdir TRIMMED```
1. ```parallel convert -trim '{}' 'TRIMMED/{}' ::: *.png```
1. ```cd TRIMMED```
1. ```ls -1 *.png  >31pngs.txt```
1. ```gm montage -verbose -adjoin -tile 7x6 +frame +shadow +label -adjoin -geometry '1023x684+0+0<' null: null: null: null: null: @31pngs.txt null: null: null: null: null: null: ig-van-2016-one-top-colour-square-per-hour-01-31january2016-square-piechart.png```

### Here's how the 24 squares per day looks!

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/29008995333/in/dateposted-ff/" title="ig-van-2016-one-top-colour-square-per-hour-01-31january2016-square-piechart"><img src="https://c6.staticflickr.com/9/8139/29008995333_1881d310f8.jpg" width="500" height="287" alt="ig-van-2016-one-top-colour-square-per-hour-01-31january2016-square-piechart"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
