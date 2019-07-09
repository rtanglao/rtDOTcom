---
layout: post
title: ' [7610] Simon Lewis''s "one step upload to Flickr" midlet works'
created: 1095436423
---
<div>
<a href="http://www.flickr.com/photo.gne?id=468512" title="photo sharing"><img src="http://www.flickr.com/photos/468512_m.jpg" alt="" style="border: solid 2px #000000;" /></a> 
<br /><a href="http://www.flickr.com/photo.gne?id=468512">1megapixel from midlet</a>  
<br />Originally uploaded by <a href="http://www.flickr.com/people/roland/">roland</a>.    
</p><p>
Simon's (he's a great programmer and friend! Thanks for the code Simon!) midlet that posts a photo immediately to <a href="http://www.flickr.com/">Flickr</a> (without any intermediate steps like storing the photo on disk or using email) works great! More later, including the source code and the midlet itself for P900, 7610 and perhaps the 6600, but here's a quick post until then.
</p><p>
Unfortunately there are limitations in the midlet (not due to Simon's programming of course!):
<br />
<br />1. It only seems to do 640x480 extrapolated to 1 megapixel instead of true 1 megapixel (perhaps this could be fixed, need to do some research, wild a*s guess: this is a bug in the Java Multimedia API?).  Compare <a href="http://www.flickr.com/photo_zoom.gne?id=468840&#38;size=m">this photo taken with Simon's midlet</a> to <a href="http://www.flickr.com/photo_zoom.gne?id=468789&#38;size=m">this photo from the native camera app</a> . Notice the jaggies in the photo from Simon's midlet.
<br />
<br />2. The 7610 doesn't implement the JSR (can't remember the number, will look it up and post the exact JSR later) which allows midlets to access the file system.  Aargh. This means that is not possible for a midlet on the 7610 to upload all the photos from the build-in camera app's folder in a batch stylee! Without the JSR, this means that to read the file system, an app must be written in C or C++, aargh!
</div>

