---
layout: post
title: Use GNU Parallel instead of xargs to run a script on wildcards and a file that is a list of files
---

## Pontifications
* Use [GNU Parallel](http://rolandtanglao.com/2016/09/12/p1-parallel-to-use-all-your-cpu-cores/) instead of xargs to run a script on wildcards and a file that is a list of files ([you can find last22locales.txt on github](https://github.com/rtanglao/rt-showfor.json/blob/master/last22locales.txt))

```bash
cat last22locales.txt | \
parallel -N 1 \
./paste-Firefox-showfor-for-a-locale.rb {} showfor.json
```
