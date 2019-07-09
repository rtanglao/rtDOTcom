---
layout: post
title: How to minify JSON using jq
---

## Pontifications
*  How to minify JSON using jq on OS X or Linux:
*  From [Using jq to minify JSON](https://nelsonslog.wordpress.com/2016/08/19/using-jq-to-minify-json/)

```bash
jq -c . < input.json >minified.json
```