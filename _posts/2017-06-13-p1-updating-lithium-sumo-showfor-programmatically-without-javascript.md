---
layout: post
title: How to update Lithium SUMO showfor.json programmatically (you have to do it one at a time, can't 100% automate it without javascript)
---

## Pontifications
* In order to programmatically get to the showfor.json for each language, you have to use javascript. The solution below uses ruby, mechanize and nokogiri and can't do javascript. (for javascript you need one or more of: [selenium](https://blog.ouseful.info/2015/12/15/grabbing-screenshots-of-folium-produced-choropleth-leaflet-maps-using-selenium/), [Watir](https://en.wikipedia.org/wiki/Watir), [Mozilla Marionette](http://rolandtanglao.com/2017/04/17/p1-marionette-to-test-in-product-urls-from-firefox-chrome/))
* So you have to do it 1 showfor.json at a time (1 for each area of the KB, i.e. once for English, once for German, once for traditional Chinese, etc). With javascript you could programmatically
* From [June 12, 2017 rt-showfor.json on github](https://github.com/rtanglao/rt-showfor.json#12june2017):

### June 12, 2017

* 1\. sample [paste-showfor.json.rb](https://github.com/rtanglao/rt-showfor.json/blob/master/paste-showfor.json.rb) run to update top level german i.e. ```Mozilla Support Community``` -> ```Mozilla Hilfe - Deutsch``` (stderr is the value BEFORE paste, stdout is the value being pasted e.g. in this example [https://github.com/rtanglao/rt-showfor.json/blob/master/showfor.json](showfor.json)), ```ARGV0``` is the URL of the Lithium showfor category e.g. [german top level is https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/category%3Ade](https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/category%3Ade) ```ARGV1``` is the minified showfor.json file:

```bash
./paste-showfor.json.rb \
https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/category%3Ade\
showfor.json
```
* 2\. read what we just changed i.e. ```Mozilla Support Community``` -> ```Mozilla Hilfe - Deutsch```

```bash
./print-showfor.json.rb \ 
https://hwsfp35778.lithium.com/t5/bizapps/bizappspage/tab/community%3Aadmin%3Asystem%3Asettings-list-editor/node-display-id/category%3Ade \
>german.json
```
* 3\. it should be what we passed in and it is!

```bash
diff -w german.json showfor.json
```