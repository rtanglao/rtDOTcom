---
layout: post
title: Get the closest colour in R from the plotrix package using color.id
---
Better than [the previous post](http://rolandtanglao.com/2015/04/28/p1-closest-color-in-r/)! From [later in the same thread of some R mailing list](http://grokbase.com/t/r/r-help/09adb1pfpm/r-general-means-of-matching-a-color-specification-to-an-official-r-color-name)

    > require(“plotrix”)
    Loading required package: plotrix
    > color.id(“#ffffff”)
    [1] “white”   “gray100” “grey100”
    > color.id(“#fefefe”)
    [1] “white”   “gray100” “grey100”