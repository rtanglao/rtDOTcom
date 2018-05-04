---
layout: post
title: "padr - an R language package to time based data more coarse grained e.g. by day or by hour instead of by second"
---

## Pontifications

* Padr looks great!
* From [Introducing Padr by Edwin Thoen from January 2017](https://edwinth.github.io/blog/padr-intro/) :

**QUOTE**

<blockquote>

I am happy to introduce the padr package, which is now available on CRAN. If you frequently work with data containing a timestamp, especially automatically created data, you might find this package helpful. It solves two problems that you can be confronted with when preparing datetime data for analysis. First, data is often recorded on too low a level for your analysis. For instance the timestamp records the moment up to the second, where you want to do the analysis on an hourly level. Second, when no events toke place there are typically no data records. This is sensible from a storage perspective, but often unhelpful for analyzing the data. When calculating a moving average for example, you want missing observations to have the value 0. You don’t want them to be lacking from your set.

</blockquote>

**END QUOTE**


