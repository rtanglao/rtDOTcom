---
layout: post
title: " My life live on Flickr courtesy of Simon's Java Midlet and my 7610"
created: 1098483755
---
<p>
[Update Sun Oct 24 2004]: I have started using the tag <a href="http://www.flickr.com/photos/roland/tags/flickrlive/">Flickr LIVE</a>! I will continue to use the 3 letter airport code (e.g. <a href="http://www.flickr.com/photos/roland/tags/yvr/">YVR</a>) to location tag my live photos as well as <a href="http://www.flickr.com/photos/roland/tags/simonsflickruploader/">simonsflickruploader</a>, <a href="http://www.flickr.com/photos/roland/tags/7610/">7610</a> and <a href="http://www.flickr.com/photos/roland/tags/cameraphone/">cameraphone</a> but my suggested and preferred tag if you do one of these yourself is FlickrLive. And there is a <a href="http://www.barbandroland.com/blog/_archives/2004/10/24/165890.html">post on barbandroland.com about this</a>.]
</p><p>
If you want to know what 's happening in my life (or at least what I am willing to reveal :-) ), you can catch <a href="http://www.flickr.com/photos/roland/tags/simonsflickruploader/">my life live on Flickr</a> courtesy of <a href="http://www.rolandtanglao.com/archives/2004/09/20/7610_random_observations_after_using_simons_7610_flickr_uploader_to_upload_80_photos">Simon's Java Midlet </a>and my 7610. Due to the slowness of Canadian GPRS there is a 6-10 minute delay between the time I take the photo and the time it appears on <a href="http://www.flickr.com/">Flickr</a>, but I think it's very cool (no Bluetooth, no USB, no iPhoto, no mobile phone upload chain of pain, no muss no fuss). Think of it as <a href="http://www.nokia.com/lifeblog">LifeBlog</a> for the rest of us or a <a href="http://www.smartmobs.com/archive/2004/09/09/the_personal_l.html">Personal Life Recorder</a> on the cheap!
</p><p>
Simon will eventually open source the code; we are not happy with the fact that the Java midlet (which I call Fup for Flickr Uploader, but the final name is of course up to Simon) seems to crash after about six 640x480 photos with a Java Null Pointer Exception and the fact that we can't take non pixelated 1 mega pixel photos.
</p><p>
We are hoping to fix the crashing problem (current strategy split the midlet in two, one for configuration, one purely for taking photos) but it looks like we can't take non pixelated 1 mega pixel photos (either the Java Multimedia API prevents this or the 7610 implementation prevents this or the cr*ppy Canadian GPRS network won't upload this much data).
</p><p>
Once we have fixed the crashing problem as best we can, we will release the code so others can join in the fun.
</p>

