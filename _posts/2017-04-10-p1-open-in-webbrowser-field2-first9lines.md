---
layout: post
title: sed to print selected lines, cut to get second field, open to open in web browser like Firefox
---

## Pontifications

* I think ```open``` only works in mac os x :-)
* Skip line 1, which is the header line, print lines 2-10, open all column B aka field 2 links from the CSV file in the web browser, i.e. Firefox:

```bash
sed -n 2,10p \
10April2017-corrected-by-vesper-mismatchedlinks-spreadsheet1.csv | \
cut -d "," -f2 | xargs -n 1 open
```
