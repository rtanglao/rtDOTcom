---
layout: post
title: "R and ggplot2: How to set literal colour values: use the 'as is' function aka I() instead of scale_colour_identity()"
---
* Please refer to my previous post: [Learnings from R, ggmap and ggplot2: I() the as is/inhibit/insulate function](http://rolandtanglao.com/2016/03/30/p1-r-ggmap-ggplot2-learnings/)        
  * Hilarious that I didn't remember my lesson from the above post from March 2016!
* Here's the diff from [sqlite-logo-text-hourly-ff-question-barcode.R](https://github.com/rtanglao/rt-r-ggplot2-ruby-experiments/blob/main/sqlite-logo-text-hourly-ff-question-barcode.R) so future me can remember better to use the 'as is' function aka `I()` to **Inhibit** ("I" is for Inhibit remember :-) !) the conversion of the `os_colours` vector to factors (see [What does the capital letter “I” in R linear regression formula mean?](https://stackoverflow.com/questions/24192428/what-does-the-capital-letter-i-in-r-linear-regression-formula-mean)) and literally use this vector as a vector of colour names instead of requiring an additional line with:`scale_colour_identity()` :-) :

```r
   print(image_df)
   p <- ggplot(image_df, aes(x, y)) +
     geom_image(aes(image = icon)) +
-    geom_label_repel(aes(label = question, colour = os_colours),
+    geom_label_repel(aes(label = question, colour = I(os_colours)),
               vjust = "inward", hjust = "inward", parse = TRUE,
               nudge_y = 2.5, nudge_x = -8, size = 3) +
-    scale_colour_identity() +
     theme_void() + expand_limits(y = c(0, 60), x = c(0, 60))
   png_filename <- sprintf("logo-text-hour-%2.2d-%s.png",
                           hour, base_name)
```