---
layout: post
title: " Nokia 6680 J2ME still doesn't allow photos larger than 640x480?!?"
created: 1121650028
---
<p>Say it ain't so Nokia! It would be totally brain dead not to be able to take full resolution pictures (1.3 megapixel on the 6680 AFAIK) from Java.  That was the case on the 7610 (<a href="http://www.rolandtanglao.com/archives/2005/02/11/huginmugin_10_j2me_flickr_uploader_for_series_60_nokia_cameraphones">which only seemed to allow 160x200 photos from Java even though the full resolution was 1 megapixel; if you requested full rez, it just did very bad extrapolation to full rez</a>). I assumed that this would be fixed in future models like the 6680 (and perhaps in newer versions of the 7610 firmware).</p><p>From <a href="http://www.thisismobility.com/blog/?p=15">Fwing Photo Upload MIDlet for 6600 and 6680</a>.:</p>
<p><b>QUOTE</b></p><blockquote>I had heard that the image resolution for captured images on the 6600 had to be the same as the display resolution when you're working in Java. Not true. If you initDisplayMode() on the VideoControl with USE_DIRECT_VIDEO then just about any parameters you pass to getSnapshot() either cause an exception or get ignored. But if you init with USE_GUI_PRIMITIVE then you can getSnapshot() in the size you want. Well, not quite the size you want. I can't get a full rez 1.3 megapixel image from the rear camera on the 6680, and I REALLY WANT ONE! The code I started with came from a sample on the Nokia site.</blockquote><p><b>UNQUOTE</b></p>



