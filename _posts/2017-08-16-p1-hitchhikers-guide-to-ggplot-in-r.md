---
layout: post
title: "Interesting scatterplots with too many points using ggplot2 and R"
---

## Pontifications

* From [R: Scatterplot with too many points](https://stackoverflow.com/questions/7714677/r-scatterplot-with-too-many-points/16122003#16122003) (things to try: alpha blending, hexagonal binning, heat maps aka rectangular binning): 

<blockquote>

I am trying to plot two variables where N=700K. The problem is that there is too much overlap, so that the plot becomes mostly a solid block of black. Is there any way of having a grayscale "cloud" where the darkness of the plot is a function of the number of points in an region? In other words, instead of showing individual points, I want the plot to be a "cloud", with the more the number of points in a region, the darker that region.

</blockquote>