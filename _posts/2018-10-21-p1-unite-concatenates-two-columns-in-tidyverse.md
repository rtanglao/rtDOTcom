---
layout: post
title: "R tidyverse function unite() concatenates two columns"
---

## Pontifications

* TIL [unite()](https://tidyr.tidyverse.org/reference/unite.html) concatenates two columns with underscore "_" being the default separator and ```separate()``` does the opposite
* [see ```unite(text, title, content, sep = " ")```](https://github.com/rtanglao/rt-kitsune-api/blob/f7205a26bab5b56c8d4ed929b0b5b1d86a6d431f/VISUALIZATIONS/firefox62-most-common-words-stop-words-removed-bar-graph.r#L11) 