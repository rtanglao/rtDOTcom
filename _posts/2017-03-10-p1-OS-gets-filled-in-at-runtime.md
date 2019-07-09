---
layout: post
title: Firefox in-product URLs support.mozilla.org/1/firefox/%VERSION%/%OS%/%LOCALE% get filled in at run-time
---

## Pontifications

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/32551494173/" title="%OS% can be WINNT or Darwin or Linux..."><img src="https://c1.staticflickr.com/4/3866/32551494173_b5798be2c4_n.jpg" width="320" height="81" alt="%OS% can be WINNT or Darwin or Linux..."></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

* On Firefox for OS X, I when I select ```Help->Firefox Help``` I see a url with ```Darwin``` in it momentarily and then the "real" url after the redirect, same with ```WINNT``` on Windows
* The ```%OS%``` values are:
    * ```Darwin``` for OSX
    * ```WINNT``` for Windows
    * ```Linux``` for Linux
    * not sure what it is for Android (maybe ```Android```?)
* nsIURLFormatter https://dxr.mozilla.org/mozilla-central/source/toolkit/components/urlformatter/nsURLFormatter.js
* The pref is ```app.support.baseURL``` and the value of that is passed to formatURL in nsURLFormatter.js
* all of the values inside ```%NAME%``` are replaced at run time when creating the url
