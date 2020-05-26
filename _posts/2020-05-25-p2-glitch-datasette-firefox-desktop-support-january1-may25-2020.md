---
layout: post
title: "HowTo: Datasette on Glitch for Firefox Desktop support questions January 1 to May 25, 2020" 
---

# Pontifications

* HowTo put the Firefox support questions on glitch from January 1-May 25, 2020 

* 1\. get the questions in CSV format into a file called sorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales into a file called [sorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales.csv](https://github.com/rtanglao/rt-kits-api2/blob/master/2020BYMONTH/sorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales.csv) :

```bash
cd /home/roland/GIT/rt-kits-api2/2020BYMONTH
../get-creator-answers-questions-for-arbitrary-time-period.rb 2020 1 1 \
2020 5 25
../print-desktop-en-us-all-oses-increasing-ids-time-url-title-content.rb \
2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales.csv csv
```

* 2\.  Per [Running Datasette on glitch](https://simonwillison.net/2019/Apr/23/datasette-glitch/):
  * "visit https://glitch.com/edit/#!/remix/datasette-csvs right now, drag-and-drop in a CSV file and watch it get served by Datasette on Glitch just a few seconds later."
  * In my case I dragged and dropped  [sorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales.csv](https://github.com/rtanglao/rt-kits-api2/blob/master/2020BYMONTH/sorted-all-desktop-en-us-2020-01-01-2020-05-25-firefox-creator-answers-desktop-all-locales.csv) into my cloned glitch instance and renamed it: [https://roland-ds1.glitch.me/](https://roland-ds1.glitch.me/)
  * And then you can do all your SQL queries goodness :-)

