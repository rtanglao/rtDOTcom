---
layout: post
title: S60 Python Success - Got Sample code to work, Nokia camera.py doesn't work
created: 1192937077
---
<p>Yay! Go my hello world program to work and finally got the OS X Bluetooth console to work. The trick is to:</p><p>ls -l /dev</p><p>and use the last tty for the screen command</p><p>e.g. if the last modified tty is tty.bt_console6</p><p>then you have to do screen /dev/tty.bt_console6</p><p>Now on to to create a program to create video in ego blogging mode (i.e. with screen facing you) using the high res camera.</p><p>I can&#39;t get the following code to work:</p>
<code>
<p>import appuifw<br /><br />import camera <br />import e32<br />from camera import *<br />&nbsp;&nbsp;&nbsp; <br />def cb(im): <br />&nbsp; try:<br />&nbsp;&nbsp;&nbsp; canvas.blit(im)<br />&nbsp;&nbsp;&nbsp; #appuifw.app.body.blit(im)<br />&nbsp; except:<br />&nbsp;&nbsp;&nbsp; appuifw.note(u&#39;cb&#39;)<br /><br />def cb2(im): <br />&nbsp; try:<br />&nbsp;&nbsp;&nbsp; appuifw.app.body.blit(im)<br />&nbsp; except:<br />&nbsp;&nbsp;&nbsp; appuifw.note(u&#39;cb2&#39;)<br /><br />import graphics<br /><br />canvas = appuifw.Canvas()<br />appuifw.app.body = canvas<br /><br />start_finder(cb)<br /><br />start_record(&#39;E:\\Python\whatever.mp4&#39;, cb2 ) <br />#stop_record() <br /></p>
</code>
<p>and I can&#39;t get the <a href="http://damonmo.googlepages.com/camera.py">Nokia camera.py </a>from <a href="http://wiki.opensource.nokia.com/projects/PyS60_python_modules">Nokia&#39;s python sample code wiki page</a> to work, help! <br /></p>
