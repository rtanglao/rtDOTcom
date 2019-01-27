---
layout: post
title: "First successful Kennedy Space Center 'patchwork quilt' suitable for tights"
---
# Pontifications


* run this script in a subdirectory of ```rt-mozlando2018-ksc```
* 
```bash
 cat ../originals.txt | ../oily-100x100px-zazzle-leg.rb 2> 26jan2019-oily100x100-stderr.txt &
 ```

 and you get this (the filename is: [interim-100x100-oily-out-row-6300.png](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/100x100OILY/interim-100x100-oily-out-row-6300.png) labelled 'interim' but it's actually the final result; the program should have terminated immediately after creating this file but it died because:<br /><br />
  [if i >= num_pixels](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/oily-100x100px-zazzle-leg.rb#L42)<br /><br /> was erroneously<br /><br />
  ```if i > num_pixels```:
 
 <a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/46164708574/in/datetaken-ff/" title="interim-100x100-oily-out-row-6300"><img src="https://farm5.staticflickr.com/4881/46164708574_8dc40d9b39.jpg" width="266" height="500" alt="interim-100x100-oily-out-row-6300"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>