---
layout: post
title: "Changing colours of ggplot2 density plots"
---

## Pontifications

* From [Changing color of density plots in ggplot2](https://stackoverflow.com/questions/7363813/changing-color-of-density-plots-in-ggplot2) the tl;dr is:

```R
m + scale_fill_manual( values = c("red","blue"))
```