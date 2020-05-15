---
layout: post
title: "How To get all Firefox Desktop SUMO KB Articles using pup" 
---

# Pontifications

* How To get all Firefox Desktop SUMO KB Articles using [pup](http://rolandtanglao.com/2020/02/16/p2-pup-for-html-like-jq-for-json/) (disclaimer this could break at any time :-)

1. Get the web page using `curl`
2. Parse the HTML :-) and find the links using `pup` (i couldn't figure out how to get the actual link from `href` so I punted and used `grep`)

```bash
curl "https://support.mozilla.org/en-US/contributors/kb-overview?product=firefox" |\
pup '#kb-overview-table tbody tr td:nth-child(1) a[href*="/en-US/kb/"]\
['href']' | grep -o '/en-US/[^\"]*' > all_relative_desktop_urls.html
```

