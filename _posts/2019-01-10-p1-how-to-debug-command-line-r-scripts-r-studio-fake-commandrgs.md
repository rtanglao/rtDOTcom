---
layout: post
title: "R and R Studio: How to debug R command line scripts with R Studio: mock commandArgs and use debugSource()"
---
# Pontifications

* Put the main function in a function e.g. ```script_main()```
* Invoke ```debug()``` on that function i.e. ```debug(script_main)```. You can see this in: [plot-antivirus-mentions-by-3weeks.r](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/plot-antivirus-mentions-by-3weeks.r)
* Create a test script that mocks up ```commandArgs``` which is the built-in command line parsing function and ```debugSource```s the file
* e.g. [testRScript.R](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/testRScript.R)

```R
commandArgs <- function(...) return(c("FF61", "2018", "6", "26", "FF62", "2018", "9", "5", "no"))
debugSource("plot-antivirus-mentions-by-3weeks.r")
rm(commandArgs)
```
* and then source ```testRScript.R``` in R Studio to debug with all the great R Studio debug utilities

* Important note when you run it using RScript, ```debug()``` is ignored! Here's how to invoke it with the command line again:

```bash
Rscript ./plot-antivirus-mentions-by-3weeks.r FF61 2018 6 26 FF62 2018 9 5 yes
```
