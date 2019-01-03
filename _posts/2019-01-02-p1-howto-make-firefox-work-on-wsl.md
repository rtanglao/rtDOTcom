---
layout: post
title: "How to make Firefox work on Windows Subsystem for Linux"
---
# Pontifications

* tl;dr install ubuntu desktop!!! and dbus and turn off multi-process(not sure this will work long-term!)

# Details on how to make Firefox work on WSL

## fix fonts, make dbus work
```bash
sudo apt-get install dbus-x11
sudo service dbus start
sudo apt-get install ubuntu-desktop
```

## turn off multi-proces
* in firefox turn off multi-process from corel (thanks!), UNSUPPORTED!!! ( from [https://support.mozilla.org/nl/questions/1167673](https://support.mozilla.org/nl/questions/1167673))

```
You can disable multi-process windows in Firefox by setting these prefs to false on the about:config page.

   browser.tabs.remote.autostart = false
   
   browser.tabs.remote.autostart.2 = false 
```

