---
layout: post
title: Reverse Engineering R joyplot code part 1 - What is p? Percentage of peak time?
---

## Pontifications
([Part 2](http://rolandtanglao.com/2017/07/11/reverse-engineering-r-joyplot-code-part2-activity-tsv/))

* Reverse engineering the [USA peak time for sports and leaisurejoyplot code from yesterday's blog post](http://rolandtanglao.com/2017/07/09/p1-instagram-joyplot-using-colours/):
* [first few lines of code](https://github.com/halhen/viz-pub/blob/master/sports-time-of-day/2_gen_chart.R):

```R
# This time, you can run this file and generate the chart with only files in this
# directory. 1_gen_data.R generates the activity.tsv file that is used in here, if you're
# looking to do similar analyses on other activtites.


library(tidyverse)
source('henrik.r') # for the horribly named theme_henrik

df <- read_tsv('activity.tsv')
```

* I still haven't figured out the ```tidyverse``` malarkey :-) ! But hopefully not critical to do so for now. I do want to learn this!
* ```henrik.r``` I guess is a theme that I can also ignore for now.
* here is the first few lines of ```[activity.tsv](https://github.com/halhen/viz-pub/blob/master/sports-time-of-day/activity.tsv)```
* I guess ```p``` is the "number of participants throughout the day compared to peak popularity```
* i.e. ```p = number_of_participants for the that time measured in hours divided by the number of participants at the peak time```?

```
activity	time	 p
Running	0.0	6.45223543281662e-5
Running	5.0	6.45223543281662e-5
Running	10.0	6.45223543281662e-5
Running	15.0	6.45223543281662e-5
Running	20.0	6.45223543281662e-5
Running	25.0	6.45223543281662e-5
Running	30.0	6.45223543281662e-5
Running	35.0	6.45223543281662e-5
Running	40.0	6.45223543281662e-5
Running	45.0	6.45223543281662e-5
Running	50.0	6.45223543281662e-5
Running	55.0	6.45223543281662e-5
Running	60.0	6.45223543281662e-5
Running	65.0	6.45223543281662e-5
Running	70.0	7.549121524369304e-5
Running	75.0	7.549121524369304e-5
Running	80.0	7.549121524369304e-5
Running	85.0	7.549121524369304e-5
Running	90.0	7.549121524369304e-5
Running	95.0	0.0
```