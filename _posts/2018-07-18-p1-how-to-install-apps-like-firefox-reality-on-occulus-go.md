---
layout: post
title: "Rough Notes: How to install apps (like Firefox Reality) on the Occulus Go using ADB on Windows 10"
---

## Pontifications

Apparently there's an easier way from cmvan that I have checkout!

* Login to developer.oculus.com
* Go to ```Oculus Go ADB Drivers```
* right click on ```android_winusb``` and then ```Install```
* Go to https://github.com/mozillareality/FirefoxReality
* click on ```Build Results``` which takes you to for example:
	* https://tools.taskcluster.net/groups/WFVLzRTLTJCf1lkt5nIEeA/tasks/WFVLzRTLTJCf1lkt5nIEeA/details
* click on the ```Run Artifacts``` tab and download the apk
* https://developer.android.com/studio/#downloads scroll to ```Command line tools only```
* https://developer.android.com/studio/releases/platform-tools
* put the Oculus Go headset on, click ok once maybe twice
*  ```adb install -r C:\Users\rtang\Downloads\FirefoxReality-oculusvr-release-signed-aligned.apk```