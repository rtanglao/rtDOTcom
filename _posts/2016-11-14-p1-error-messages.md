---
layout: post
title: Software Error Messages don't often help (e.g. R - single value instead of array value error message)
---
## Pontifications

The following example is from the R language but I've found misleading error messages in every computer language and operating system I've ever used.

* ```In if (is.na(col)) col <- par("col") : the condition has length > 1 and only the first element will be used```
* What was this error message from? It was from col being multiple element valued i.e. an array instead of single valued variable. Would it be possible for the error message to be something more helpful like ```col was expected to be an integer or color name single element variable instead of a 360 length array``` 

