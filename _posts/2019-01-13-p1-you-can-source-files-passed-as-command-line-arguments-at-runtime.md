---
layout: post
title: "R: you can source files you pass as command line arguments at run time!"
---
# Pontifications

* This wasn't obvious to me :-) ! Maybe it's my C/C++ brain damage in action !!!

```bash
 % Rscript testSourceCommandLine.R testSourceAtRunTime.R
── Attaching packages ─────────────────────────────────────── tidyverse 1.2.1 ──
✔ ggplot2 3.1.0     ✔ purrr   0.2.5
✔ tibble  1.4.2     ✔ dplyr   0.7.8
✔ tidyr   0.8.2     ✔ stringr 1.3.1
✔ readr   1.3.1     ✔ forcats 0.3.0
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
[1] "testSourceAtRunTime.R"
[1] 1
```

* code from [testSourceCommandLine.R](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/testSourceCommandLine.R)

```r
library(tidyverse)
args <- commandArgs(TRUE)
file_to_source <- args[1]
print(file_to_source)
source(file_to_source)
print(x)
```

* code from [testSourceAtRunTime.R](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/testSourceAtRunTime.R)

```r
x = 1
```