---
layout: post
tags : [r, rlang, jupyter, python, instagram, instagram vancouver, instagram vancouver 2014, top colour]
title: R Language Jupyter notebook to load my instagram 2014 top colour dataset
---
The following (hmmm jekyll won’t render my html tag correctly; until I get it fixed, you can find the [proper html rendering of the notebook here](https://dl.dropboxusercontent.com/u/361757/R_JUPYTER_NOTEBOOKS/How%20to%20load%20the%20top%20colour%20instagram%202014%20dataset.html)) is an Jupiter(fka iPython) notebook showing how to download and install [my instagram Vancouver 2014 top colour dataset](http://rolandtanglao.com/2015/05/03/p1-instagram-vancouver.2014-topcolour-dataset-now-on-cran/) in R


    r = getOption(“repos”) # hard code the UK repo for CRAN
    r[“CRAN”] = “http://cran.uk.r-project.org”
    options(repos = r)
    rm(r)

    install.packages(“ig.vancouver.2014.topcolour”)
    
    The downloaded source packages are in
    	‘/private/var/folders/v0/4gc0rf6x5t5bsjt77skb0_y00000gn/T/RtmpbTwMy1/downloaded_packages’

    library(ig.vancouver.2014.topcolour)

    data(“topcolour.ig.vancouver.2014”)

    str(topcolour.ig.vancouver.2014)

    ‘data.frame’:	245736 obs. of  2 variables:
     $ colour: Factor w/ 245736 levels “#000000”,”#000002”,..: 245736 244100 244077 242458 240150 245689 245650 244087 244088 239521 …
     $ count : int  8010 6894 3861 3734 3229 2926 2719 2390 2154 2114 …

    head(topcolour.ig.vancouver.2014, 5)


<table>
<thead><tr><th></th><th scope=col>colour</th><th scope=col>count</th></tr></thead>
<tbody>
	<tr><th scope=row>1</th><td>#FFFFFF</td><td>8010</td></tr>
	<tr><th scope=row>2</th><td>#FEFEFE</td><td>6894</td></tr>
	<tr><th scope=row>3</th><td>#FEFCFF</td><td>3861</td></tr>
	<tr><th scope=row>4</th><td>#FBFFFF</td><td>3734</td></tr>
	<tr><th scope=row>5</th><td>#F7FFFF</td><td>3229</td></tr>
</tbody>
</table>





    
