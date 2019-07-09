---
layout: post
title: It's 2016, can I please debug Javascript, R, Julia and Haskell like a 1987 Xerox Lisp Machine?
---
## Pontifications

* I don't want to use print statements or separate debuggers like xdb or gdb or [rr](http://robert.ocallahan.org/2014/03/introducing-rr.html). I just want to be able to go backwards and forwards, change variables, stop the execution, change the code and the values of variables and continue backwards and forwards just like we did in my AI course at the University of Waterloo on a Xerox Lisp Work station in 1987! How hard can it be :-) ?
* I will settle for being able to debug R when passing command line arguments in! Can't believe [R Studio doesn't support that](https://support.rstudio.com/hc/en-us/articles/205612627-Debugging-with-RStudio)!!!!!!!
* You have to call ```system("Rscript yourscript.R arg1 arg2")``` or some other such [kludgery](http://stackoverflow.com/a/25148513) and you end up debugging outside R Studio!
