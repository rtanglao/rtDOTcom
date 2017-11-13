---
layout: post
title: " [7610] Random observations after using Simon's 7610 Flickr uploader to upload
  80 photos"
created: 1095711961
---
<p>
Here are some random observations and comments on the state of Java and mobile phones and the mobile Internet after spending the weekend uploading <a href="http://www.flickr.com/photos/roland/tags/simonsflickruploader/">over 40 photos</a> with Simon's cool prototype one step upload (after approx. 10 clicks) app:
</p><p>
0. It is very cool to upload (even at 640x480) photos in one step in real time to <a href="http://flickr.com/">Flickr</a> despite the comments that follow below (thanks Simon and thanks Fido and thanks Nokia for providing the phones and software and service that makes this possible).
</p><p>
1. The mobile internet (or should I say the GPRS version of the mobile internet) is too slow.  It takes almost a minute from the time I take the picture until the time it's successfully uploaded to Flickr (and this is for a 640x480, imagine how long it will take for a 1 megapixel image).  This will be fixed in time. Bring on Edge and 3G. Does anybody know when Edge or 3G will be available in Vancouver?
</p><p>
2. The Java VM on the 7610 is too fragile.  After uploading about 40 photos using Simon's app, it crashes with an out of memory error.  This may be due to the fact that Simon's app is a prototype and therefore has a memory bug, but isn't Java's memory manager supposed to handle this :-)?
</p><p>
3. The Java VM on the 7610 either doesn't have enough memory or the 7610 doesn't have enough memory to allow many apps to run simultaneously. If I run Opera and Simon's uploader, it crashes sooner with the dreaded Symbian out of memory error, -4.
</p><p>
4. The Java Multi media API as implemented on the 7610 <a href="http://discussion.forum.nokia.com/forum/showthread.php?s=218e3037a5e405429a76c56a900bd92b&#38;threadid=18988&#38;highlight=%2Acapture+video%2A">doesn't seem to allow the capture of true 1 megapixel images</a> (perhaps the answer is in <a href="http://www.forum.nokia.com/ndsCookieBuilder?fileParamID=2778">this camera midlet PDF from Nokia</a> but after a brief skim I couldn't find anything relevant about image capture size) Why not? Any further clues on how to set the camera to take true 1 mega pixel images from the multimedia API  would be appreciated. Simon nor I can find a way to do this.
</p><p>
My next experiment will be to try <a href="http://www.picostation.com/">Picoblogger</a> ; an MT, MetaWeblogAPI  and some day Flickr compatible moblogging app. And once Simon has finished some small improvements, I will post his Flickr uploader app here.
</p>

