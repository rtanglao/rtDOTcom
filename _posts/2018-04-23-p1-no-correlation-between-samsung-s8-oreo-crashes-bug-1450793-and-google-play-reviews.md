---
layout: post
title: "No correlation between Samsung S8 Devices in bug 1450793 (crashing after Oreo update) and Google Play Store 1 and 2 star reviews for those same S8 devices"
---

## Pontifications

* Following on from yesterday's post, [R Code to plot unanswered google play reviews using ggplot2 including code to rotate x axis labels so they are readable](http://rolandtanglao.com/2018/04/22/p1-r-code-to-plot-count-of-unanswered-1-and-2-star-reviews/) :
* There doesn't seem to be a correlation between Samsung S8 Devices in [bug 1450793](https://bugzilla.mozilla.org/show_bug.cgi?id=1450793)  (crashing after Oreo update) and Google Play Store 1 and 2 star reviews for those same S8 devices
* If there was a correlation you'd see a spike in S8 device 1 and 2 star reviews in Mid March-early April 2018 just like we saw a spike in crashes for these devices in bug 1450793

Here's the code [https://github.com/rtanglao/rt-fennec-gplay/blob/master/23april2018-r-scratch.R](https://github.com/rtanglao/rt-fennec-gplay/blob/master/23april2018-r-scratch.R):

```R 
count_p_red_device = year_month_day_device_all_languages_unreplied_one_and_two_star_reviews_star_last_updated_language %>% 
  add_count(Device, sort = TRUE) %>% 
  filter(n > 100)
p_count_red_device = 
  ggplot(
    data = count_p_red_device,
    aes(x=yyyy_mm_dd, fill="red")) +
  geom_bar(stat = "count")+
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) + 
  facet_wrap(~ Device)

#I would bet that is our issue.  Here are the affected model numbers. They probably use a different chip, or something.
#U.S. S8 SM-G950U1 (dreamqlteue)
#U.S. S8 plus SM-G955U1 (dream2qlteue)
#Canadian S8 SM-G950W (dreamqltecan)
#Canadian S8+ SM-G955W (dream2qltecan)
#Australian Galaxy S8 SCV36

s8_family_bug_1450793_p = year_month_day_device_all_languages_unreplied_one_and_two_star_reviews_star_last_updated_language %>% 
    filter(
      (Device == "dreamqlteue") |
      (Device == "dream2qlteue") | 
      (Device == "dreamqltecan") |
      (Device == "dream2qlteue") |
      (Device == "dream2qltecan") |
      (Device == "SCV36")
    )
p_count_pink_s8_family_device = 
  ggplot(
    data = s8_family_bug_1450793_p,
    aes(x=yyyy_mm_dd, fill="pink")) +
  geom_bar(stat = "count")+
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) + 
  facet_wrap(~ Device)
```
### Plot showing no correlation between s8 crashes and s8 reviews on the google play store (crashes started occurring with oreo upgrade but there's no corresponding spike in 1 and 2 star reviews)

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/39845714550/in/datetaken-public/" title="aka no correlation between s8 crashes and s8 reviews on the google play store (crashes started occurring with oreo upgrade but there&#x27;s no corresponding spike in 1 and 2 star reviews)s8_family_bug_1450793"><img src="https://farm1.staticflickr.com/883/39845714550_198881975a_n.jpg" width="320" height="291" alt="aka no correlation between s8 crashes and s8 reviews on the google play store (crashes started occurring with oreo upgrade but there&#x27;s no corresponding spike in 1 and 2 star reviews)s8_family_bug_1450793"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>