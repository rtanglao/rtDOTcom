---
layout: post
title: "How to use SQLite to search all the Firefox and Thunderbird kb articles including the HTML (sadly Markdown not available)"
---

* Using datasette lite, load the CSV files.
  * [Firefox](https://lite.datasette.io/?csv=https%3A%2F%2Fraw.githubusercontent.com%2Frtanglao%2Frt-kits-tb-api%2Fmain%2Fdetails-firefox-kb-title-slug-all-articles.csv#/data/details-firefox-kb-title-slug-all-articles): Load [https://github.com/rtanglao/rt-kits-tb-api/blob/main/details-firefox-kb-title-slug-all-articles.csv](https://github.com/rtanglao/rt-kits-tb-api/blob/main/details-firefox-kb-title-slug-all-articles.csv) into datasette lite
  * [Thunderbird](https://lite.datasette.io/?csv=https%3A%2F%2Fraw.githubusercontent.com%2Frtanglao%2Frt-kits-tb-api%2Fmain%2Fthunderbird-kb-title-slug-all-articles-details.csv): Load [https://github.com/rtanglao/rt-kits-tb-api/blob/main/thunderbird-kb-title-slug-all-articles-details.csv](https://github.com/rtanglao/rt-kits-tb-api/blob/main/thunderbird-kb-title-slug-all-articles-details.csv) into datasette lite

### Previously

* May 8, 2020: [Thanks  to Simon Willison's lite.datasette.io you can now query any SQLite data  with CORS headers anywhere and share the query URL with others so it  can spread virally :-)!  (e.g. 2021 Firefox SUMO Support questions) on  any web browser including desktop, iOS and Android](http://rolandtanglao.com/2022/05/08/p1-query-my-firefox-201-sumo-support-data-from-your-web-browser-mobile-desktop-no-server-no-app-required/)        
