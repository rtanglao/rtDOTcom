---
layout: post
title: "How To get all Firefox Desktop SUMO KB Articles using pup WITHOUT using grep by using 'attr{href}'" 
---

# Pontifications

* How To get all Firefox Desktop SUMO KB Articles using [pup](http://rolandtanglao.com/2020/02/16/p2-pup-for-html-like-jq-for-json/) (disclaimer this could break at any time :-)

1. Get the web page using `curl`
2. Parse the HTML :-) and find the links using `pup` 

```bash
curl "https://support.mozilla.org/en-US/contributors/kb-overview?product=firefox" |\
pup '#kb-overview-table tbody tr td:nth-child(1) a[href*="/en-US/kb/"]\
attr{href}'  > all_relative_desktop_urls.html
```

See the earlier, grep version: [How To get all Firefox Desktop SUMO KB Articles using pup](http://rolandtanglao.com/2020/05/14/p1-how-to-get-all-firefox-desktop-urls-using-pup/)

