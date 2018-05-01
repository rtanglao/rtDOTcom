---
layout: post
title: "R Tips: How to force the Y Axis breaks in ggplot2 to be integers from Stack Overflow: How to display only integer values on an axis using ggplot2"
---

## Pontifications

* use ```scale_y_continuous()``` (from [https://github.com/rtanglao/rt-fennec-gplay/blob/master/30april2018-r-scratch.R](https://github.com/rtanglao/rt-fennec-gplay/blob/master/30april2018-r-scratch.R) )
* found the above on Stack Overflow somewhere :-) i.e.  [How to display only integer values on an axis using ggplot2](https://stackoverflow.com/questions/15622001/how-to-display-only-integer-values-on-an-axis-using-ggplot2/39877048#39877048)

```R
scale_y_continuous(
    breaks = function(x) unique(
      floor(pretty(seq(0, (max(x) + 1) * 1.1))))) 
```



