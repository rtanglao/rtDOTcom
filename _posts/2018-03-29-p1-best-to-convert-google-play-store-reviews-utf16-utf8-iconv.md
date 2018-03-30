---
layout: post
title: "Google Play Store Review spreadsheets are UTF-16 not UTF-8, best to convert to UTF-8 using iconv"
---

## Pontifications
 
 * Following up from [yesterday's Windows files are UTF-16 NOT UTF8, how to read them in ruby: 'rb:bom|utf-16'](http://rolandtanglao.com/2018/03/28/p1-windows-files-are-utf16-not-utf8-how-to-read-them-in-ruby/):
	 * Google Play Store Review spreadsheets are in UTF-16 not UTF-8 for some strange reason.
	 * Most tools like ruby expect UTF-8 and work better with UTF-8
	 * Therefore convert to UTF-8 as follows using iconv:
	 
	 ```bash
	 iconv -f UTF-16 -t UTF-8 utf16-spreadsheet-from-gplay-reviews.csv >utf8-spreadsheet-from-gplay-reviews.csv
	 ```
