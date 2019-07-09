---
layout: post
title: How to debug video playback issues on Firefox for Android
created: 1408054453
---
<ul><li>brew install android-platform-tools</li><li>adb shell am start -a android.activity.MAIN -n org.mozilla.fennec/.App --es env0 NSPR_LOG_MODULES=MediaDecoder:5</li><li>adb logcat gecko</li><li>supporting material:</li><ul><li><a href="https://wiki.mozilla.org/Mobile/Fennec/Android">https://wiki.mozilla.org/Mobile/Fennec/Android</a><br />"Arguments and Environment Variables "<br />--es env# VAR=VAL<br />where VAR=NSPR_LOG_MODULES=MediaDecoder:5 (the string "MediaDecoder" was found using a google search of DXR</li><li><a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1047567">https://bugzilla.mozilla.org/show_bug.cgi?id=1047567</a></li><li><a href="http://webcompat.com/issues/275">http://webcompat.com/issues/275</a></li></ul></ul>
