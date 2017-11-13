---
layout: post
title: How to make a named character vector in R 
---
From [stack overflow](http://stackoverflow.com/questions/19265172/converting-two-columns-of-a-data-frame-to-a-named-vector) assuming you have a column called "colour" in "tt":

```R
colour_named_vector <-setNames(as.character(tt$colour), 
tt$colour)
> colour_named_vector
  #FFFFFF   #FEFEFE   #FEFCFF   #FBFFFF   #F7FFFF   #FFFDFF 
"#FFFFFF" "#FEFEFE" "#FEFCFF" "#FBFFFF" "#F7FFFF" "#FFFDFF" 
> typeof(colour_named_vector)
[1] "character"
```

