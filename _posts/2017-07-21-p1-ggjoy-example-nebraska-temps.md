---
layout: post
title: "Lincoln Nebraska temperature ggjoy() code is what i want (just need fill colour to be set to the month)"
---

## Pontifications

Yay for fab example code!
    
* The [ggjoy vignette](https://cran.r-project.org/web/packages/ggjoy/vignettes/introduction.html) has this modified Lincoln Nebraska ggjoy() example (from [original blog post by Austin Wehrwein](http://austinwehrwein.com/data-visualization/it-brings-me-ggjoy/) )

```R
ggplot(lincoln_weather, aes(x = `Mean Temperature [F]`, y = `Month`)) +
  geom_joy(scale = 3, rel_min_height = 0.01) +
  scale_x_continuous(expand = c(0.01, 0)) +
  scale_y_discrete(expand = c(0.01, 0)) +
  labs(title = 'Temperatures in Lincoln NE',
       subtitle = 'Mean temperatures (Fahrenheit) by month for 2016\nData: Original CSV from the Weather Underground') +
  theme_joy(font_size = 13, grid = T) + theme(axis.title.y = element_blank())
  ```
  * I just have to (easy peasy right :-) ?):
      *  change the months to colours
      * change the fill colour to the colours
      * change the "mean temperature" to 24 counts of the colours (1 count / hour)