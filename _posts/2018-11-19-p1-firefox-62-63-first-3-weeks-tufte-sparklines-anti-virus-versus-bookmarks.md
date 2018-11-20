---
layout: post
title: "Firefox 62 and 63 First 3 weeks Tufte Sparklines: anti-virus versus bookmarks"
---

## Pontifications
* There is a bug in [print-daynum-issuetype-issuecount.rb](https://github.com/rtanglao/rt-kitsune-api/blob/master/print-daynum-issuetype-issuecount.rb), need to count "anti-virus" as well as "antivirus" and "anti virus" !
* And I am probably missing some anti-virus "googlewhacks" :_)
* R code which uses the CSV from ```print-daynum-issuetype-issuecount.rb```:
  * [12november2018-ff62-tufte-sparklines](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/12november2018-ff62-tufte-sparklines.r)
  * [13november2018-ff63-tufte-sparklines.R)](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/13november2018-ff63-tufte-sparklines.R)
### Output

* observations: bookmarks appears more frequently in FF63 and FF62, need to add in FF 61 and FF 60

**FF62:**<br />

* graph FF62 using [12november2018-ff62-tufte-sparklines.r](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/12november2018-ff62-tufte-sparklines.r) 

![ff62-1st-3-weeks-antivirus-bookmarks-tufte-sparkline.png](https://github.com/rtanglao/rt-kitsune-api/raw/master/VISUALIZATIONS/ff62-1st-3-weeks-antivirus-bookmarks-tufte-sparkline.png)

**FF63:**<br />

* graph FF63 using [13november2018-ff63-tufte-sparklines.R](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/13november2018-ff63-tufte-sparklines.R) 

![ff63-1st-3-weeks-antivirus-bookmarks-tufte-sparkline.png](https://github.com/rtanglao/rt-kitsune-api/raw/master/VISUALIZATIONS/ff63-1st-3-weeks-antivirus-bookmarks-tufte-sparkline.png)
