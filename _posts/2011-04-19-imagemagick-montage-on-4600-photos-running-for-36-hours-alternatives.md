---
layout: post
title: ImageMagick montage on 4600 photos running for 36 hours! Alternatives?
created: 1303224635
---
<p>I am trying to create a <a href="http://wordpress.mrreid.org/moviebarcode/">barcode</a> like the <a href="http://www.flickr.com/photos/roland/5497246053/">barcode I did for Gastown</a> out of 4600 1 pixel by 720 pixel jpeg photos using the <a href="http://www.imagemagick.org">ImageMagick</a> montage command as follows:</p><blockquote><p>montage -geometry +0+0 -tile x1 *.jpg foobarcode.png</p></blockquote><p>It's been running for 36 hours and still hasn't finished, anybody got a faster alternative? Clearly I am "unencumbered by knowledge" :-) when it comes to image processing. My bet is there's another newer open source toolkit that will do this faster.</p>
