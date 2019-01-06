---
layout: post
title: "Volker Weber: How to delete Windows 10 'crapware' using 'remove-appxpackage'"
---
# Pontifications

* OMG I didn't know about ```remove-appxpackage```
* Read the whole thing: [Setting up a new Windows 10 machine](https://vowe.net/archives/017656.html) <--- tl;dr ```Get-AppxPackage|? name -like *Xbox*|remove-appxpackage```