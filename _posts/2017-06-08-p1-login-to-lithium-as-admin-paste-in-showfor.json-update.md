---
layout: post
title: UPDATE--Login to Lithium as Admin, paste in showfor.json
---

## Pontifications
* Apropos to yesterday's [Login to Lithium as Admin, paste in showfor.json](http://rolandtanglao.com/2017/06/07/p1-login-to-lithium-as-admin-paste-in-showfor.json/), it looks like you can go directly to the url:
    1. Login 
    1. Go to the community admin url e.g. [https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/tkb-board%3APersonalizeFirefox](https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/tkb-board%3APersonalizeFirefox) i.e. ```Mozilla Support English``` -> ```Firefox``` -> ```Personalize Firefox```
    2. Paste in [showfor.json](https://github.com/rtanglao/rt-showfor.json/blob/master/showfor.json) here and submit the form
* So all we need is a a script that takes 2 parameters:
    * 1\. URL like [https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/tkb-board%3APersonalizeFirefox](https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/tkb-board%3APersonalizeFirefox)
    * 2\. showfor.json filename (could be tailored to the product e.g. thunderbird only articles should probably only have showfor.json with thunderbird in it? no need for firefox for android and mac and win and desktop for example)
