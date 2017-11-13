---
layout: post
title: Get the data right, lessons from R
---
## Pontification :-)
* If the data isn't right (especially if it contains not a number i.e. ```NA```), then it won't work, especially with ggplot2.
* If the data isn't right you won't get much of an error message. Use ```str()```, ```head()```, ```typeof()``` and really look at your data
* Write the simplest possible test program to make sure your data is correct 
* You basically never need loops, yay! Hooray for ```apply()```, ```sapply()``` et al

