---
layout: post
title: Bug Labs Release 1.4.2 - asynchronous GPS API broken, synchronous works but
  requires polling
created: 1252899951
---
<p><object classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" type="application/x-shockwave-flash" data="http://www.flickr.com/apps/video/stewart.swf?v=71377" height="400" width="400"><param name="flashvars" value="intl_lang=en-us&amp;photo_secret=ff746cef8c&amp;photo_id=3787917184&amp;flickr_show_info_box=true"> <param name="movie" value="http://www.flickr.com/apps/video/stewart.swf?v=71377"> <param name="bgcolor" value="#000000"> <param name="allowFullScreen" value="true"><embed type="application/x-shockwave-flash" src="http://www.flickr.com/apps/video/stewart.swf?v=71377" bgcolor="#000000" allowfullscreen="true" flashvars="intl_lang=en-us&amp;photo_secret=ff746cef8c&amp;photo_id=3787917184&amp;flickr_show_info_box=true" height="400" width="400"></object></p> <p>Back in August using <a href="http://www.bugcommunity.com/wiki/index.php/R1.4.1_Release_notes">Bug Labs Release 1.4.1</a>, Simon Lewis and I got his Bug Labs bug identicon app that generates identicons based on GPS coordinates to work. Unfortunately that used the Bug Labs synchronous API i.e. polling which runs down the battery. The working version is 1.0.3 and you can see the output of 1.0.3 in the video above.</p><p>It's still broken in Bug Labs Release 1.4.2&nbsp; Full yak shaving details after the jump!</p><p><!--break--></p><p>So the next step was to try the asychronous API. It didn't work. The Concierge component framework would crash:</p> <pre>root@bug:~# tail -f /var/log/concierge.log
[Thu Jan 01 00:01:39 GMT 1970] [INFO] CoolApp 1.1.1: code != lastCode
[Thu Jan 01 00:01:39 GMT 1970] [INFO] IdenticonComponent: Initialized image and got sun.awt.qt.QtImage@86b11f3a
[Thu Jan 01 00:01:39 GMT 1970] [INFO] IdenticonComponent: image == sun.awt.qt.QtImage@86b11f3a
[Thu Jan 01 00:01:39 GMT 1970] [INFO] CoolApp 1.1.1: CoolApp.newIdenticon(...)
[Thu Jan 01 00:01:39 GMT 1970] [INFO] CoolApp 1.1.1: CoolApp.newIdenticon(...): Writing /usr/share/java/./storage/default/39/data/identicons/4915.17N_1234.19W.png
[Thu Jan 01 00:01:40 GMT 1970] [INFO] CoolApp 1.1.1: Got position update
[Thu Jan 01 00:01:40 GMT 1970] [INFO] CoolApp 1.1.1: Latitude[0.8596597123194212 rad] Longitude[-2.1480144386300855 rad]
[Thu Jan 01 00:01:40 GMT 1970] [INFO] CoolApp 1.1.1: Computing digest
[Thu Jan 01 00:01:40 GMT 1970] [INFO] CoolApp 1.1.1: Got digest
[Thu Jan 01 00:01:40 GMT 1970] [INFO] CoolApp 1.1.1: code == lastCode

II) every other time it didn't appear to run, it just hangs after it starts

ar]:
java.lang.LinkageError: trying to redefine class com.buglabs.bug.jni.common.CharDevice (bad class loader?)
    at java.lang.Class.addToLoaderCache(Native Method)
    at java.lang.Class.loadSuperClasses(Unknown Source)
    at java.lang.ClassLoader.defineClass(Unknown Source)
    at ch.ethz.iks.concierge.framework.BundleClassLoader.findOwnClass(Unknown Source)
    at ch.ethz.iks.concierge.framework.BundleClassLoader.findDelegatedClass(Unknown Source)
    at ch.ethz.iks.concierge.framework.BundleClassLoader.findClass(Unknown Source)
    at java.lang.ClassLoader.loadClass(Compiled Method)(Unknown Source)
    at java.lang.ClassLoader.loadClass(Unknown Source)
    at java.lang.Class.loadSuperClasses(Unknown Source)
    at java.lang.ClassLoader.defineClass(Unknown Source)
    at ch.ethz.iks.concierge.framework.BundleClassLoader.findOwnClass(Unknown Source)
    at ch.ethz.iks.concierge.framework.BundleClassLoader.findClass(Unknown Source)
    at java.lang.ClassLoader.loadClass(Compiled Method)(Unknown Source)
    at java.lang.ClassLoader.loadClass(Unknown Source)
    at java.lang.ClassLoader.loadClassInternal(Unknown Source)
    at com.buglabs.bug.input.pub.InputEventProvider.run(Unknown Source)
    at java.lang.Thread.startup(Unknown Source)
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registering info service.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet /support
STARTING file:./com.buglabs.bug.service.jar
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet /service
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet at /service.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered resources /
STARTING file:./com.buglabs.bug.program.jar
[Thu Aug 06 21:46:14 UTC 2009] [INFO] UserAppManager init: false
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet /program
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet /configuration
STARTING file:./com.buglabs.bug.module.jar
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet /module
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet at /module.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet /package
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Registered servlet at /package.
STARTING file:./com.buglabs.bug.bmi.jar
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.gps (0001) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.camera (0005) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.lcd (0003) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.motion (0002) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.vonhippel (0007) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.audio (000A) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.wifi (0008) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Added modlet factory com.buglabs.bug.module.bugbee (0009) to map.
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Creating pipe /tmp/eventpipe
[Thu Aug 06 21:46:14 UTC 2009] [INFO] Execution Completed.  Response:
[Thu Aug 06 21:46:15 UTC 2009] [INFO] Initializing existing modules
[Thu Aug 06 21:46:15 UTC 2009] [INFO] Registering existing module with message: 0003 0 0 ADD
[Thu Aug 06 21:46:15 UTC 2009] [INFO] Started modlet from factory com.buglabs.bug.module.lcd...
[Thu Aug 06 21:46:15 UTC 2009] [INFO] Registering existing module with message: 0001 0 1 ADD
[Thu Aug 06 21:46:15 UTC 2009] [INFO] GPSModlet setting active (external) antenna
CoolAppServiceTracker: start
[Thu Aug 06 21:46:16 UTC 2009] [INFO] CoolApp 1.1.1: CoolApp.start()
[Thu Aug 06 21:46:16 UTC 2009] [INFO] Started modlet from factory com.buglabs.bug.module.gps...
[Thu Aug 06 21:46:16 UTC 2009] [INFO] Listening to event pipe. /tmp/eventpipe
STARTING file:./com.buglabs.bug.event.jar
[Thu Aug 06 21:46:16 UTC 2009] [INFO] Registered servlet /event
[Thu Aug 06 21:46:16 UTC 2009] [INFO] Registered servlet at /event.
STARTING file:./com.buglabs.bug.slp.jar
---------------------------------------------------------
  Framework restarted in 7.075 seconds.
--------------------------------------------------------- 
</pre> <p>So I had high hopes for the recently introduced Bug Labs Release 1.4.2. I hoped that the asynchronous API would be fixed. Based on the <a href="http://www.bugcommunity.com/wiki/index.php/R1.4.2_Release_notes">1.4.2 release notes</a>, I didn't think it was fixed and today I am blogging this to confirm it's still broken in 1.4.2 Instead of a crash with a nice traceback, I now just get signal 11 with no traceback:</p> <pre>Poky Linux 3.1 on BUG
root@bug:~# tail -f /var/log/concierge.log 
RESTORED BUNDLE file:./com.buglabs.bug.program.jar
RESTORED BUNDLE file:./com.buglabs.bug.module.jar
RESTORED BUNDLE file:./com.buglabs.bug.bmi.jar
RESTORED BUNDLE file:./com.buglabs.bug.event.jar
RESTORED BUNDLE file:./com.buglabs.bug.slp.jar
RESTORED BUNDLE file:/usr/share/java/apps/CoolApp.jar
STARTING file:./service-tracker.jar
STARTING file:./com.buglabs.osgi.shell.jar
Process #3983 received signal 11
Process #3983 being suspended

</pre>
